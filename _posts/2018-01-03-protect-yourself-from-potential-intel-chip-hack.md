---
layout: post
title: "Protect yourself from Intel CPU hack"
description: "Keep yourself safe from potential exploits of Intel Kernel Hack"
categories: [security]
tags: [tutorial,security]
---

## What happened in this early on new year?

I woke of this morning with flooding news of Kernel memory leaking on Intel Chip and its essential consequence problem.

Of course, that's super big problem to deal with, and there are unlimited amount security problems that you have to endanger with because of it. So let me wrap up what happens and quick action to decrease the amount of damage you may unwantedly receive.

You may not get the detail of this problem, but this article is just to help you stay safer from the storm.

## What the heck is it, and the danger you may face with it.

The bug lies in all modern Intel processors those produced by that Evil Corporation; the company of which, their CEO recently [sold a lot of stock](https://news.ycombinator.com/item?id=16055851). Meaning that you can not do anything, absolutely nothing with it, unless you turn off your computer and get some sleep, then switch to a laptop with AMD processor. And you should only work on iPhone, iPad, Android devices from now on to keep you safe from the wrath of Intel.

The bug allows any user to observe to some extent the contents of protected kernel memory areas. Any program includes websites from browsers, may be able to sniff the memory of other applications, where your password, keys, and all sorts of secret information from yours (your private photo as well if you're browsing it). In a better scenario, Hackers may be possible to inject a piece of codes in memory and create a better version of SQL injection.

In a bigger view, if you are in IT industry, prepare for the surge of CPU, with the [patch from Linux](https://lkml.org/lkml/2017/12/4/709), you should expect the service will consume extra CPU. Note that the fix on PostgreSQL slows the database [something like 20%](https://www.postgresql.org/message-id/20180102222354.qikjmf7dvnjgbkxe@alap3.anarazel.de). If all services take additional 20% CPU like PostgreSQL, meaning that Amazon and Google need to prepare extra 20% more computer (Just a no-brainer number). Including maintenances and reboots, your services, if they are big enough, will suffer some hiccups.

### How do I lower the risk for myself?

Install patches as soon as possible. In the meantime:

- You must know that all kind of scripts includes Javascript may be able to read your credential. Use your smartphone to surf webs. Don't visit any unknown website. Don't install new software unless you have to.
- Change your password often, use two factors login as much as possible
- Avoid using the credit card and other payment systems.

### How do I limit the damage to my services?

- Ask your admin/dev-ops team to prepare for more CPU consumption.
- Limit your IP access if possible
- Start monitor who login/out
- If you're using AWS, you've probably received an email about the maintenance scheduled for Jan 5th, 2018, keeping up with it.
- If you're using Azure, their VMs are expected to get rebooted on Jan 10th 2018

### Final words:

See video below and don't panic, enjoy 2018 with me.
{% raw %}
<iframe class="youtube" width="560px" height="315px" src="https://www.youtube.com/embed/ewe3-mUku94?start=1800" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
{% endraw %}
