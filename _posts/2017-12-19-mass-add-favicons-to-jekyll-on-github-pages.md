---
layout: post
title: "Mass-add favicons to Jekyll on Github pages."
description: "Tutorial how to add multiple favicons to Jekyll easily."
categories: [blog]
tags: [blog,jekyll,favicon,tutorial]
---

At the [previous post](/blog/2017/12/18/tech-blog-gfm-on-your-domain-over-ssl/), I have guided you how to set up a scalable blog post using Github flavored markdown. With a proper setup on Cloudflare, you can have a free and scalable blog system over SSL on your own purchased domain.
However, as one of the oldest branding strategy on the internet, the favicon is the thing that we are missing off. This blog post's purpose is to guide you to set up your favicon effortlessly.
### Step 1, find your icon.
First and foremost, you need an icon for your website, and please don't tell me where to get it. As a hint, you can get a free icon on [findicons.com](https://findicons.com) or [iconfinder.com](https://www.iconfinder.com)
### Step 2, mass generating your favicons
There is a bunch of services those generate favicons for iOS, Android, Website, Window Phone or others device, the one I use the most is [favicomatic](http://www.favicomatic.com/). Go ahead and upload your icon and select `Every damn size, sir!`.
### Step 3, Copy to your assets
Download the generated favicons and put it into `/assets/images` folder. It should look like this:
```
assets/images/
├── apple-touch-icon-114x114.png
├── apple-touch-icon-120x120.png
├── apple-touch-icon-144x144.png
├── apple-touch-icon-152x152.png
├── apple-touch-icon-57x57.png
├── apple-touch-icon-60x60.png
├── apple-touch-icon-72x72.png
├── apple-touch-icon-76x76.png
├── code.txt
├── favicon-128.png
├── favicon-16x16.png
├── favicon-196x196.png
├── favicon-32x32.png
├── favicon-96x96.png
├── favicon.ico
...
```
### Step 4, Add metadata to your blogs
Modify your `_includes/common/meta.html` file and paste the following content:

~~~ html
<link rel="apple-touch-icon-precomposed" sizes="57x57" href="/assets/images/apple-touch-icon-57x57.png" />
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="/assets/images/apple-touch-icon-114x114.png" />
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="/assets/images/apple-touch-icon-72x72.png" />
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="/assets/images/apple-touch-icon-144x144.png" />
<link rel="apple-touch-icon-precomposed" sizes="60x60" href="/assets/images/apple-touch-icon-60x60.png" />
<link rel="apple-touch-icon-precomposed" sizes="120x120" href="/assets/images/apple-touch-icon-120x120.png" />
<link rel="apple-touch-icon-precomposed" sizes="76x76" href="/assets/images/apple-touch-icon-76x76.png" />
<link rel="apple-touch-icon-precomposed" sizes="152x152" href="/assets/images/apple-touch-icon-152x152.png" />
<link rel="icon" type="image/png" href="/assets/images/favicon-196x196.png" sizes="196x196" />
<link rel="icon" type="image/png" href="/assets/images/favicon-96x96.png" sizes="96x96" />
<link rel="icon" type="image/png" href="/assets/images/favicon-32x32.png" sizes="32x32" />
<link rel="icon" type="image/png" href="/assets/images/favicon-16x16.png" sizes="16x16" />
<link rel="icon" type="image/png" href="/assets/images/favicon-128.png" sizes="128x128" />
<meta name="application-name" content="&nbsp;"/>
<meta name="msapplication-TileColor" content="#FFFFFF" />
<meta name="msapplication-TileImage" content="mstile-144x144.png" />
<meta name="msapplication-square70x70logo" content="mstile-70x70.png" />
<meta name="msapplication-square150x150logo" content="mstile-150x150.png" />
<meta name="msapplication-wide310x150logo" content="mstile-310x150.png" />
<meta name="msapplication-square310x310logo" content="mstile-310x310.png" />
~~~

### 5. Check your works
Build your pages with `bundle exec jekyll serve` and navigate to `localhost:4000` to check your work, fix errors if have.
After that push to Github to enjoy your favicons! Yummy!