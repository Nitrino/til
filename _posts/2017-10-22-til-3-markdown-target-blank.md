---
layout: post
title:  "[#3] Markdown target blank"
categories: common
---
In HTML for open a link in the new tab uses `target` attribute with value `_blank`

{% highlight html %}
<a href="http://nitrino.io" target="_blank">My home page</a>
{% endhighlight %}

The same behavior in Markdown can be obtained with this code:

{% highlight markdown %}
[My home page](http://nitrino.io){:target="_blank"}
{% endhighlight %}
