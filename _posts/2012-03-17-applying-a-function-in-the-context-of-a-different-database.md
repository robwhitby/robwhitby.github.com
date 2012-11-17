---
author: Rob
title: Applying a function in the context of a different database
excerpt:
layout: post
---

As far as I know there are two ways to access a different database from xquery – `xdmp:eval` and `xdmp:invoke`, both of which take an options node specifying the database context. `xdmp:eval` is best avoided because it requires the query be a string. `xdmp:invoke` can only invoke main modules, and these are often nothing but proxies to library functions. Both functions require that any parameters are declared as external variables, with one big limitation – sequences are not supported.

So it would be really useful if you could also call a specific function directly. One way to do this would be if `xdmp:apply` accepted the same options node:

{% highlight xqy %}
xdmp:apply(
  $function,
  <options xmlns="xdmp:eval"><database>{xdmp:database("another-db")}</options>,
  $params
)
{% endhighlight %}