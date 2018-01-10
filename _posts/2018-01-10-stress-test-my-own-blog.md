---
layout: post
title: "Stress test my Jekyll blog."
description: "Stress test my own free Jekyll blog up to 100 virtual users."
categories: [blog]
tags: [blog,stresstest]
---

## Why stress test my blog?

If you follow the previous articles on [blogging](https://tonny.me/blog/categories/#blog), I claimed that we create a scalable blog on HTTPS for free, this article provides you more with details and share the strategy of the stress test and the result.

## Stress test strategy

### The cache

My blog serves through a CDN layer called CloudFlare, and to make the result of the stress test useful; I disabled the cache on `/blog/*`. Otherwise, I'm going to do a meaningless stress test on CloudFlare. With this setting, only assets include static content like javascript, CSS, images are cached to improve speed, the content request will hit the AWS instance provided by Github, which I assume is the weakest one.

### Scenario

I made myself an assumption that every user will spend the time to read three blog articles. Therefore, every virtual user will request three random posts, and to mimic the standard browser during the session, memory cache is available.

Virtual users will come from 5 different regions, following the following table

|---
| Weighting | Region
|-|-
| 20% | US West
| 20% | US East
| 20% | Ireland
| 20% | Singapore
| 20% | Sao Paulo

The limit is set to 100 virtual users.

## The test result

### Summary

|---
| Maximum Running Vusers | 100
| Total Transfer | 98.31 MB
| Throughout | Average: 165.58 KB/s Peak:1.09 MB/s
| Total Requests | 39,323
| Requests per Second | Average: 64.68/s Peak:182.00/s
| Average Response Time | Average: 0.176s HTML: 0.233s
| Total Passed scenarios | 3,746
| Total Failed scenarios |   10

Some notable measurements

- Almost no error, only ten scenarios failed because the testing instance in AWS ran out of memory.
- Super low response time
- Quite good RPS

### Region based summary for total webpage

|---
| Region | Minimum | Average | Median | Std.Deviation | 90 Percent | Pass | Fail
| - | - | - | - | - | - | - | -
| Asia Pacific (Singapore) | 1.279s | 1.467s | 1.388s | 0.244s | 1.716s | 810 | 0
| EU (Ireland) | 0.967s | 1.119s | 1.085s | 0.178s | 1.280s | 826 | 0
| South America (Sao Paulo) | 1.492s | 1.595s | 1.495s | 0.206s | 1.562s | 623 | 0
| US East (N. Virginia) | 0.794s | 0.953s | 0.939s | 0.115s | 1.047s | 658 | 0
| US West (Northern California) | 0.950s | 1.164s | 1.156s | 0.084s | 1.272s | 829 | 0

90% total webpage load time is less than 2 seconds, quite a good performance

## Final thought

Without CDN for `/blog/*`, and without any fee, the ability to deliver up to 182 Requests per second for less than 2 seconds for all region is ridiculous good. Turning up the cache for `/blog/*` will serve requests than that. It's more than enough for a personal blog.