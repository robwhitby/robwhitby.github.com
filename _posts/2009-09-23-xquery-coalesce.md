---
author: Rob
title: XQuery coalesce
excerpt:
layout: post
---

A little trick I picked up recently..

XQuery doesn’t have a coalesce function so I was writing code like:

{% highlight xqy %}
if ($x) then $x else "default value"
{% endhighlight %}`

But there’s a nicer way which shows why there’s no need for a coalesce function:

{% highlight xqy %}
($x, "default value")[1]
{% endhighlight %}

Everything is a sequence…