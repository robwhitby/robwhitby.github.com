---
author: Rob
title: 'MarkLogic searches - stemmed vs unstemmed'
excerpt: It turns out that setting a cts:query to be stemmed or unstemmed has a nasty side-effect ...
layout: post
tags: 
  - XQuery
  - MarkLogic
---
It turns out that setting a cts:query to be stemmed or unstemmed has a nasty side-effect that can be a real problem if you are searching content in multiple languages. In theory a stemmed search should always return the same or more results than an unstemmed query, right? Well that’s true, as long as both queries are searching the same content…

And here’s the problem: In MarkLogic, stemmed queries only search content in one language.

{% highlight xqy %}
  cts:search(
    fn:doc(),
    cts:word-query("chicken", "unstemmed")
  )
{% endhighlight %}

This will search for the word ‘chicken’ in all documents, regardless of language.

{% highlight xqy %}
cts:search(
  fn:doc(),
  cts:word-query("chicken", "stemmed")
)
{% endhighlight %}

This will search for stems of the word ‘chicken’ in documents of the **database default language only**.

I was shocked by this, turns out all my searches were omitting the 10% or so of documents not in English! I wrongly presumed that all content would be searched but stemming would only have an effect in english content.

So what do you do if you need to use stemming but also want to search content across multiple languages? There is no fantastic solution but here are 2 hacks that get the job done:

1. Set all xml:lang attributes everywhere to the same language, and store the actual language somewhere else instead. This is nice because it doesn’t require changing any xquery, but may introduce complications further down the line.

2. Modify all stemmed queries to an or query – stemmed or unstemmed.

{% highlight xqy %}
cts:search(
  fn:doc(),
  cts:or-query(
    cts:word-query('chicken', 'stemmed'),
    cts:word-query('chicken', 'unstemmed')
  )
)
{% endhighlight %}

This searches en documents with stemming, and then all documents without stemming. It will incur a performance hit, as the query is more complex. How bad will depend on your content, index settings etc. On my database the impact was negligible.

Which option is better I’m not sure – neither are ideal. Here is a discussion I had about this issue on the MarkLogic mailing list:  
<http://markmail.org/thread/e5hdnjg5rcayxxhl>