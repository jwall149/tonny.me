---
layout: post
title: "Control SSL in gcloud with kube-lego"
description: "How to add and update tls certificate with kube-lego in gcloud"
categories: [gcloud,kubernetes]
tags: [kube-lego,ssl,kubectl,ingress,gce]
---

## Forewords and mission

We are using [https://github.com/jetstack/kube-lego](Kube-lego) to register and update certification automatically from Let's Encrypt. While setting up the server, there some problems and pitfalls that I faced, I'm going to list here so you can avoid.

Before talking about the goal, let me share some specs of our system. We have a website for a lot of customers and need to set up an https subdomain on our primary domain for each of them for each of them. Each content is different for each customer, but we handle all those logic inside a single application.

The ultimate goal is set up and add more domain to the system if required. And we're going to add a new subdomain to the ingress automatically for each customer.

## The ingress file

{% highlight yml linenos=table %}
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: random
  namespace: prod
  annotations:
    kubernetes.io/ingress.class: gce
    kubernetes.io/tls-acme: 'true'
    kubernetes.io/ingress.global-static-ip-name: random-prod
spec:
  tls:
    - secretName: random-secret-prod
      hosts:
        - abc.example.com
        - cde.example.com
  backend:
    serviceName: random
    servicePort: 8080
{% endhighlight %}

---

Line 8:  This is required in order for `kube-lego` to be active, `kubernetes.io/tls-acme` must be set to `'true'`. Do not change it to `true`(boolean),  it need to be a string.

---

Line 9:  `kubernetes.io/ingress.global-static-ip-name: random-prod`:

The IP name `random-prod` must be set up beforehand. You can create a new one with this command:

`gcloud compute addresses create random-prod`

---

Line 11:

Each object inside `TLS`  supports only 1 hostname, never provide two different root hostname like this:

~~~ yaml
spec:
  tls:
    - secretName: random-secret-prod
      hosts:
        - abc.example.com
        - cde.moreexample.com
~~~

---

Line 12: `secretName` is the secret name to store the TLS certificates, therefore must be provided.

---

### Update Ingress

When you have new domain, you can add domain like this

~~~ yaml
spec:
  tls:
    - secretName: random-secret-prod
      hosts:
        - abc.example.com
        - cde.example.com
        - efg.example.com
~~~

But remember that

`kubectl apply -f newfile.yaml` does not work

Use
`kubectl replace -f newfile.yaml` instead.
