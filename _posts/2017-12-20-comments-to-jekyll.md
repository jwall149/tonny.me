---
layout: post
title: "How to add comment to static Jekyll webpage"
description: "Tutorial show the solution to add dynamic comments to static Jekyll website."
categories: [blog]
tags: [tutorial,jekyll,disqus,comment]
---

## Why do we need the comment?

Comments are one of the undoubtedly effective methods to increase interaction between blog's author and viewer since the first day of Web 2.0. Comments raise the revisiting frequency of viewer, giving useful feedback to the writer to create better content for the future blog. However, there's a problem with our [previous blog architecture](/blog/2017/12/18/tech-blog-gfm-on-your-domain-over-ssl/) `Jekyll` generates static webpage to Github pages. How do we solve the dynamic content problem of this design?

`Disqus` is my answer to the difficulty raise above. The reason I chose `Disqus` over other alternatives are:

- Easy to set up, just register an account at [Disqus](https://disqus.com), and you then have everything
- The viewer has multiple choice of login, well organized and well interacted with other social accounts as well.
- Pretty good UI and easy to use, also SPAM control with `Disqus` behave exceptionally well; almost you do not have to do anything.
- Free, it cost nothing to set up.

Here are the step to set it up:

### Step 1. Register a Disqus account

Go to `Disqus` website and sign up an account, then create a webpage. You need to note the `short name` that `Disqus` asks you to enter.

### Step 2. Set up the configuration

Go to file `_config.yml` and add or overwriting the following
~~~
disqus:
  shortname: tonnyme
  site_url: https://tonny.me
~~~
Remember the short name in Step 1? Replace `tonnyme` with yours. Also, replace `site_url` with your site URL, this is important to prevent duplicated comments.

### Step 3

Replace file `_includes/common/disqus.html` completely with the following content:
{% highlight javascript linenos=table %}
{% raw %}
<script>
var disqus_config = function () {
    this.page.url = "{{ site.disqus.site_url }}{{ page.url }}";
    this.page.identifier = "{{ page.id }}";
};

var loadDisqus = function() {
    var d = document, s = d.createElement('script');
    s.src = 'https://{{ site.disqus.shortname }}.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
};

$(document).ready(function () {
    $('.comments .show-hidden').on('click', function () {
        loadDisqus()
        $(this).remove();
    });

    if (/\#comments/.test(location.hash)) {
        $('.comments .show-hidden').trigger('click');
    }
});
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endraw %}
{% endhighlight %}

[^1]: _includes/common/disqus.html

### That is it
Deploy and enjoy comment :)

