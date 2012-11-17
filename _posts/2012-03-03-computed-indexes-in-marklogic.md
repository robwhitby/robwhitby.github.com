---
author: Rob
title: Computed indexes in MarkLogic
excerpt:
layout: post
---

Imagine we have a load of XML in different schemas that we want to query as one dataset. Because MarkLogic is schema agnostic we can just chuck it all in and start querying. That’s great, except if we need to query by date for example, and the documents have different ways of expressing their date:

{% highlight xml %}
<doc id="1">
  <date>2012-03-01</date>
</doc>

<doc id="2">
  <date-published>2012-03-01</date-published>
</doc>

<doc id="3">
  <date>01 March 2012</date>
</doc>
{% endhighlight %}

We could handle multiple element QNames by using a field, but the non xs:date format in doc 3 is a bigger problem.

**Current Solution**

The usual approach is to perform some normalisation, or “enrichment” at or before ingestion to create a value specifically for indexing:

{% highlight xml %}
<doc id="1">
  <date>2012-01-01</date>
  <index:date>2012-01-01</index:date>
</doc>

<doc id="2">
  <date-published>2012-02-01</date-published>
  <index:date>2012-02-01</index:date>
</doc>

<doc id="3">
  <date>01 March 2012</date>
  <index:date>2012-03-01</index:date>
</doc>
{% endhighlight %}    

This is fine until our query requirements change. We then have to change the enrichment script and either re-ingest everything or run a batch job with corb or similar to update every document.

**Computed Index Idea**

Instead of having to enrich the data at ingestion, why not do the work at index time instead? Similar to computed columns in relational dbs. I imagine something like extending the range index options to allow specifying a function to be executed on each fragment to get the index value:

{% highlight xqy %}
declare function compute-date-index($fragment as node()) as xs:date?
{
  (: logic to get the date - same as used to enrich documents with index:date :)
};
{% endhighlight %}  

We’d then need some new functions to access the index, new cts query constructors like cts:computed-range-query() etc. The trade off would be increased index time – and I’ve got no idea what sort of effect even the most simple function would have. The benefit would be far greater flexibility and ease of creating/managing indexes. It would also allow an index to be based on an XPath expression, useful when the schema has repeated element QNames whose meaning is dependant on context.

{% highlight xml %}
<doc id="1">
  <date>2012-01-01</date>
  <reference>
  	<id>2</id>
  	<date>2012-02-01</date>
  </reference>
</doc>
{% endhighlight %}    

I’m sure there are loads of implications I’m unaware of, so would be great to get people’s thoughts.