---
layout: post
title: "Tech blog with gfm on your own domain over ssl"
description: "A zero cost but scalable tech blog with markdown on a custom domain over SSL"
categories: [blog]
tags: [blog,jekyll,github,cloudflare,github-pages,scalable,markdown]
---

So you finally come here to look for a solution to your blog? Well, at least how to build your blog the most comfortable way. So did I.

A month ago, I figured out that just some edit of my everyday documents that I wrote for every project I join in, can make an excellent blog post. Sometimes I spend a day to look for a solution to a problem, and if I publish it, the solution may save thousands of hours of people yearning for an answer on the internet.

What were the requirements for the blog solution I want to accomplish? It must be  `GitHub-markdown-format`, and `Scalable`, and `secure` and `free`.

Going straight forward to the solution, I'm using `Github-pages` to store contents, `Jekyll` as the blog engine, `CloudFlare` as the `SSL Endpoint` and `Content Delivery Network`.

Jekyll provides `GitHub-markdown`, of course, the must, because that's the format I love. That's the format I'm writing my documents and draft every day, and no question ask when all I need is mindless copying the note to the blog.  Needlessly, `Github-markdown` will also provide `code block` and `code highlighting`, which indeed help on visualization. More than that, the combination of `CloudFlare` with `Github-pages` is totally free of charge, even with free SSL, and scalable.

Step:

### Fork a Jekyll website
Go to [Jekyll Themes](http://jekyllthemes.org/) and choose the theme you like, then navigate to its Github page. After that, you can fork the repository to yours.
### Change content and check local build
You're required to have `Ruby version 2.2 or after`, to do this task. Run
```
gem install bundler
```
To install bundler. After that run
```
bundle install
```
To install the required gems. To start `Jekyll` server, start with
```
bundle exec jekyll serve
```
To compile all markdown to HTML.
### Push and check
After that, all you need to do is push to Github `master` or `gh-pages` branch. Your blog will be available at `your_user_name.github.io` . Visit `Settings > Github pages` to set custom domain