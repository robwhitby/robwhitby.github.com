---
author: Rob
title: Applying a function in the context of a different database - MarkLogic 7 update
excerpt:
layout: post
---


A couple of years ago I wrote about how useful it would be to [apply a function in the contect of a different database][originalpost]. At that time there were two choices - eval a string or invoke a main module. But things have changed since then, in MarkLogic 7 there are a  couple of new functions:

{% highlight xqy %}
xdmp:invoke-function(
   function() { xdmp:document-insert("doc",$content), xdmp:commit() },
   <options xmlns="xdmp:eval"><database>{xdmp:database("another-db")}</options>
)


xdmp:spawn-function(
   function() { xdmp:document-insert("doc",$content), xdmp:commit() },
   <options xmlns="xdmp:eval"><database>{xdmp:database("another-db")}</options>
)
{% endhighlight %}

Spawn differs from invoke in that the function will be executed asynchronously on the task server.

The documentation explains the details better than I could [xdmp:invoke-function][docsinvokefn], [xdmp:spawn-function][docsspawnfn]. And check out [taskbot][taskbot] for a great example of these new functions in action.


[originalpost]: /2012/03/17/applying-a-function-in-the-context-of-a-different-database.html
[docsinvokefn]: http://docs.marklogic.com/xdmp:invoke-function
[docsspawnfn]: http://docs.marklogic.com/xdmp:spawn-function
[taskbot]: https://github.com/mblakele/taskbot