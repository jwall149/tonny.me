---
layout: post
title: "Switch from Disqus to Facebook comment."
description: "How to switch comment system from Disqus to Facebook."
categories: [blog]
tags: [jekyll,disqus,facebook,comment]
---

## Switching from Disqus to Facebook comment, why?

In the [previous blog](/blog/2017/12/20/comments-to-jekyll/), I showed you the reason I chose `Disqus` for the comments. After weeks, I just realize:

- Free version of Disqus is too slow to load
- Unstable, not reliable
- Ads, I do not want ads from Disqus

So I decided to switch from Disqus to Facebook comments to enjoy Facebook spam filter. Also, I can free myself from ads as well.

There are a few steps that you need to set Facebook's comments on a Jekyll website

## Set up a Facebook app

Facebook requires an AppID to use their comments system; you can [sign up one](https://developers.facebook.com/quickstarts/?platform=web) here for your website.

Eventually, you will need a [privacy website like this](/about/privacy) to publish your app. After that, you can use the Comment feature.

## Set up with Jekyll

You need to change several places to achieve this

### First add the configuration into `_config.yml`

~~~ yaml
comment:
  site_url: https://tonny.me
  facebook:
    app_id: '12309812301823'
~~~

### Add `_includes/common/loading.html`:

{% highlight html linenos=table %}
{% raw %}
<div class="lds-css ng-scope">
  <div style="width:100%;height:100%;margin:0 auto;" class="lds-facebook">
    <div></div> <div></div> <div></div> </div>
<style type="text/css">@keyframes lds-facebook_1 {
  0% {top: 36px; height: 128px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
@-webkit-keyframes lds-facebook_1 {
  0% {top: 36px; height: 128px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
@keyframes lds-facebook_2 {
  0% {top: 41.99999999999999px; height: 116.00000000000001px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
@-webkit-keyframes lds-facebook_2 {
  0% {top: 41.99999999999999px; height: 116.00000000000001px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
@keyframes lds-facebook_3 {
  0% {top: 48px; height: 104px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
@-webkit-keyframes lds-facebook_3 {
  0% {top: 48px; height: 104px; }
  50% {top: 60px; height: 80px; }
  100% {top: 60px; height: 80px; }
}
.lds-facebook {position: relative; }
.lds-facebook div {position: absolute; width: 30px; }
.lds-facebook div:nth-child(1) {
  left: 35px;
  background: #8cd0e5;
  -webkit-animation: lds-facebook_1 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  animation: lds-facebook_1 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  -webkit-animation-delay: -0.2s;
  animation-delay: -0.2s;
}
.lds-facebook div:nth-child(2) {
  left: 85px;
  background: #376888;
  -webkit-animation: lds-facebook_2 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  animation: lds-facebook_2 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  -webkit-animation-delay: -0.1s;
  animation-delay: -0.1s;
}
.lds-facebook div:nth-child(3) {
  left: 135px;
  background: #826b88;
  -webkit-animation: lds-facebook_3 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
  animation: lds-facebook_3 1s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook {
  width: 200px !important;
  height: 200px !important;
  -webkit-transform: translate(-100px, -100px) scale(1) translate(100px, 100px);
  transform: translate(-100px, -100px) scale(1) translate(100px, 100px);
}
</style></div>
{% endraw %}
{% endhighlight %}

### Add file `_includes/common/facebook.html` with the following content:

{% highlight html linenos=table %}
{% raw %}
<div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = 'https://connect.facebook.net/en_US/sdk.js#xfbml=1&version=v2.11&appId={{ site.comment.facebook.app_id }}';
  js.onload = function() {
    FB.Event.subscribe("xfbml.render", function(response) {
        loading = document.getElementsByClassName('lds-css')[0]
        loading.style.display = 'none';
    });
  }
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
{% endraw %}
{% endhighlight %}

### Change the `div.misc-content` in `_layouts/post.html`

{% highlight html linenos=table %}
{% raw %}
<div class="misc-content">
    {% if site.comment.facebook.app_id and page.comments != false %}
        {% include common/loading.html %}
        {% include common/facebook.html %}
        <div class="comments">
            <div class="fb-comments" data-href="{{ site.comment.site_url }}{{ page.url }}" data-numposts="5" data-width="100%"></div>
        </div>
    {% endif %}
</div>
{% endraw %}
{% endhighlight %}

## That is it

Enjoy Facebook comment, don't forget to comment on this page
