---
layout: post
title: "Test with goroutine and redis"
description: "Redis pubsub testing with multiple goroutines"
categories: [golang]
tags: [testing,goroutine,golang,redis]
---

## Testing with goroutine and redis

So notice the function in redis

~~~ go
func (r *redisPubsub) Subcribe(ctx context.Context, topic string, invocation pubsub.Invocation) error {
	if topic == "" {
		return status.Errorf(codes.InvalidArgument, "Topic should not be empty")
	}

	if invocation == nil {
		return status.Errorf(codes.InvalidArgument, "Invocation should not be empty")
	}

	// If already subscribed, then add to the list of invocations
	if _, ok := r.pubsubs[topic]; ok {
		r.invocations[topic] = append(r.invocations[topic], invocation)
		return nil
	}

	go func(rp *redisPubsub, x context.Context, t string, i pubsub.Invocation) {
		rp.subcribe(x, t, i)
	}(r, ctx, topic, invocation)

	return nil
}
~~~

Subscribe function inits a goroutine to repeatedly loop and wait for messages published from redis.

Also, I want to test subscribe and redis working correctly.

### Problem and first try

~~~ go
func TestPubSub(t *testing.T) {
	t.Parallel()
	ps, err := NewRedisPubsub("localhost:6379")
	if err != nil {
		// Can not connect to local
		log.Infoln("Can not connect to local redis server to test")
		return
	}
	log.Infoln("Connected to local redis server... Start testing redis")

	ms1 := ""
	var err1, err2 error
	ms2 := ""

	f1 := func(payload []byte, err error) {
		ms1 = string(payload)
		err1 = err
	}
	f2 := func(payload []byte, err error) {
		ms2 = string(payload)
		err2 = err
	}

	ctx := context.Background()
	topic := "topic"

	ps.Subcribe(ctx, topic, f1)
	ps.Subcribe(ctx, topic, f2)

	ps.Publish(ctx, topic, "hungry")
	time.Sleep(time.Second * 2)
	if ms1 != "hungry" {
		t.Fatal("Can not publish")
	}

}
~~~

with `redis-cli monitor` tools we can see the sequence:

~~~ bash
$ redis-cli monitor
OK
1513834144.738129 [0 [::1]:52892] "ping"
1513834144.738677 [0 [::1]:52892] "publish" "topic" "hungry"
1513834144.739505 [0 [::1]:52894] "subscribe" "topic"
1513834144.739544 [0 [::1]:52893] "subscribe" "topic"
~~~

You can notice that even we call Subscribe first, the publish got to the redis first before we subscribe; hence the test always yields the error.

### Solution

Of course, I do not want to change any code in Subscribe to provide callback after subscribe, so I need to find a way to work around

- Keep publishing once every 500 milliseconds
- Redirect both callbacks into single channel to avoid concurrency
- Capture the first message from channel, and looking forward to seeing that message again
- Make a timeout to cancel the test after 10 seconds and mark it fail

In the end, the codes look like:

~~~ go
func TestPubSub(t *testing.T) {
	t.Parallel()

	testOk := false

	ps, err := NewRedisPubsub("localhost:6379")
	if err != nil {
		// Can not connect to local
		log.Infoln("Can not connect to local redis server to test")
		return
	}
	log.Infoln("Connected to local redis server... Start testing redis")

	msgChan := make(chan string)

	// Catch message and put to single queue
	f1 := func(payload []byte, err error) {
		msgChan <- string(payload)

	}
	f2 := func(payload []byte, err error) {
		msgChan <- string(payload)
	}

	ctx, cancel := context.WithCancel(context.Background())
	topic := "topic"

	ps.Subcribe(ctx, topic, f1)
	ps.Subcribe(ctx, topic, f2)

	// Publish forever for every half a second
	go func(ctx context.Context) {
		c := 0
		for {
			select {
			case <-ctx.Done():
				return
			default:
				pmsg := fmt.Sprintf("%s_%d", "original", c)
				ps.Publish(ctx, topic, pmsg)
				c++
				time.Sleep(time.Millisecond * 500)
			}
		}
	}(ctx)

	// 10 second time out
	go func() {
		time.Sleep(10 * time.Second)
		cancel()
	}()

	// Now catch first message from msgChan and find its pair
	firstMsg := ""
	for {
		select {
		case <-ctx.Done():
			if !testOk {
				t.Fatalf("Can not get two published messages")
			}
			return
		case msg := <-msgChan:
			log.Infof("Get broadcasted message: %s\n", msg)
			if firstMsg == "" {
				firstMsg = msg
			} else {
				if msg == firstMsg {
					testOk = true
				}
				cancel()
			}
		}
	}
}
~~~

Of course, it works like a charm.

```
[ `go test -test.run="^TestPubSub$"` | done: 2.138786698s ]
	INFO: 2017/12/21 15:58:03 Connected to local redis server... Start testing redis
	INFO: 2017/12/21 15:58:03 RedisPubsub: Receive from topic topic, message: original_0
	INFO: 2017/12/21 15:58:03 Get broadcasted message: original_0
	INFO: 2017/12/21 15:58:03 Get broadcasted message: original_0
	PASS
```
