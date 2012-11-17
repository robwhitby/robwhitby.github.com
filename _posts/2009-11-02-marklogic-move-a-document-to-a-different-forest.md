---
author: Rob
title: 'MarkLogic: Move documents to new forests'
excerpt:
layout: post
---

Our development database had been allowed to grow unchecked and the single forest was well over the recommended 200GB max size. So I created 2 new forests to move all the documents into (I think that’s faster than moving half into one new forest and then having loads of deleted fragments to clean up in the initial forest).

The technique is to first set the initial forest as delete-only and then re-insert all the documents without changing them. Inserting a document at a URI that already exists will normally update it, but because the forest is delete-only, it will be saved in one of the new forests instead.

Here’s the code to move a single document

{% highlight xqy %}
xquery version '1.0-ml';

declare function local:document-move-forest($uri as xs:string)
{
  local:document-move-forest(
    $uri,
    xdmp:database-forests(xdmp:database())
  )
};

declare function local:document-move-forest($uri as xs:string,
  $forest-ids as xs:unsignedLong*)
{
  xdmp:document-insert(
    $uri,
    fn:doc($uri),
    xdmp:document-get-permissions($uri),
    xdmp:document-get-collections($uri),
    xdmp:document-get-quality($uri),
    $forest-ids
  )
};
{% endhighlight %}

This will keep the document’s permissions, collections and quality. And the properties document is maintained and moved with it.

Call this function using [Corb][1] on all the documents in the original forest, and then just remove the now empty forest.

 [1]: http://developer.marklogic.com/svn/corb/trunk/README.html