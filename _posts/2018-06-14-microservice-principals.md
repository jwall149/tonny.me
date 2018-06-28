---
layout: post
title: "Microservice design principles"
description: "Key principles of designing a microservice-oriented system"
categories: [microservice]
tags: [microservice,principal,design]
---

## Monolithic service, a.k.a spaghetti service

Many things have changed in these 20 years of software development. Yes, many things changed, but the only thing stays the same is `The need for growth`.

It's very usual to see two versions of service: An user-facing website and an internal administration tool. And the whole architecture follows a very same pattern like this: a router stands in front listens to request and redirect it to computation instances, all of the server instances access the same database.

{% xdot svg %}
digraph {
    rankdir=LR;
    subgraph cluster_0 {
        Router;
    }
    subgraph cluster_1 {
        label="Servers";
        Router -> s1;
        Router -> s2;
        Router -> s3;
        rank=same;
    }

    subgraph cluster_2 {
    	s1 -> Database;
    	s2 -> Database;
    	s3 -> Database;
        rank=same
    }
}
{% endxdot %}

However, these kinds of monolith services introduce difficulties in the term of scaling. After the service is released and got positive feedback from the customer, the providers try to add features, fixing bugs... and more engineers need to work on the product. Imagine that a hundred of people eating the same spaghetti, it is fricking hard to coordinate teams to build, and maintain a single software component. There are common problems such as conflicts on releases and reintroduction of bugs, which consume most of the team's strength and spirit. Beyond that, adding/removing people require a lot of training and preparation time as well.

## Moving toward Microservices

Many companies, after realize the tremendous amount of effort to scale up a monolith system, try to split into microservices, so that the teams can focus on fewer and smaller isolated modules. This separation encourages the engineers to build, update, and deploy an autonomous and explicit module of a particular requirement without the fear of interfering with the rest of the system.

However, microservices is not a holy grail of service development, because it introduces some problems that you will never have to deal with while working with a monolithic system.

I'm preparing for a meetup on `Moving toward Microservices` in the mid of July, 2018. If you want have some fun with beer, and know more about Microservices, please provide your email address for detail notification.

{% raw %}
<!-- Begin MailChimp Signup Form -->
<link href="//cdn-images.mailchimp.com/embedcode/classic-10_7.css" rel="stylesheet" type="text/css">
<style type="text/css">
    #mc_embed_signup{background:#fff; clear:left; font:14px Helvetica,Arial,sans-serif; }
    /* Add your own MailChimp form style overrides in your site stylesheet or in this style block.
       We recommend moving this block and the preceding CSS link to the HEAD of your HTML file. */
</style>
<div id="mc_embed_signup">
<form action="https://tonny.us11.list-manage.com/subscribe/post?u=017ce8aff4e61cff908bb9fc2&amp;id=d79badb190" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="validate" target="_blank" novalidate>
    <div id="mc_embed_signup_scroll">
    <h2>Enter your email for meetup notification</h2>
<div class="mc-field-group">
    <label for="mce-EMAIL">Email Address </label>
    <input type="email" value="" name="EMAIL" class="required email" id="mce-EMAIL">
</div>
<div class="mc-field-group">
    <label for="mce-FNAME">Full Name </label>
    <input type="text" value="" name="FNAME" class="required" id="mce-FNAME">
</div>
    <div id="mce-responses" class="clear">
        <div class="response" id="mce-error-response" style="display:none"></div>
        <div class="response" id="mce-success-response" style="display:none"></div>
    </div>    <!-- real people should not fill this in and expect good things - do not remove this or risk form bot signups-->
    <div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_017ce8aff4e61cff908bb9fc2_d79badb190" tabindex="-1" value=""></div>
    <div class="clear"><input type="submit" value="Subscribe" name="subscribe" id="mc-embedded-subscribe" class="button"></div>
    </div>
</form>
</div>

<!--End mc_embed_signup-->
{% endraw %}

### Network latency
Now instead of calling a function, you need to call in a different server on a different network since microservice is a naturally distributed system, and you should never expect your `function call` to happen too fast.

### Maintainability
Bug tracking is not easy, especially since you have to trace through different services. Having more server and more services indicates more monitoring, more maintenance.

### Consistency
We have to admit the fact that the data is split between services, and could be inconsistent for a period. Having eventual consistency takes time and effort to implement. We will talk about this in detail on a different blog post.

## So what's the point?

The good thing about a microservice-oriented architecture is when designed correctly, can provide any mid to large sized company a very flexible system that scales up resiliently. But to the most important, it is critical to have the fundamental principles in mind when designing a microservice architecture. Otherwise, we are going to end up with a half-baked system running on different machines which generate more problem than a well-designed monolith solution.

### Independent of services
All services should be designed independently and working autonomously around a business domain, and they should be loosely coupling to each other. All components of a service should be highly cohesive.
- Develop and, deploy independently
- Decentralize services, no SPOF
- Publish only services' interface

### Automate everything
Moving from `function`  to different independent services mean that you are willing to accept maintenance overhead. Automation helps you a lot on code maintaining, speeding up service implementation.

- Infrastructure automation
- Testing automation
- CI/CD
- Monitoring automation

### Availablity over consistency
The natural characteristic of a microservice system is the decentralization. Hence splitting data across multiple services, multiple databases helps teams govern the flows and business logic of their domains. Consistency will introduce bottom neck, single point of failure, and you should not try to achieve it. If you have to ensure the transaction at all cost, take a look yourself at `eventual consistency`. We will talk about that in a different chance.

### Vertical approaching
When you build a service, avoid creating one service that acts as the core bus of multiple parts or even the whole system. This method is a so-called horizontal approach.
Avoid it approaching by all means.
Instead, start with your smallest service you can think of to bold up your momentum, like sending email, user authentication, reporting sales...