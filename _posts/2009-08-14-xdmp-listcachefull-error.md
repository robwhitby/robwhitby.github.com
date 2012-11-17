---
author: Rob
title: XDMP-LISTCACHEFULL error
excerpt:
layout: post
---

Today I found some queries were erroring with:

XDMP-LISTCACHEFULL: List cache full on host …

Googling “LISTCACHEFULL” returns a paltry [1 result][1] – someone asking about the error on the MarkLogic mailing list but getting no response. Great.

I simplified the query down to the part causing the error:

```xqy
cts:search(
  fn:doc(),
  cts:element-query(
    fn:expanded-QName("http://www.springer.com/app/meta", "OrgName"),
    cts:word-query("university of exeter", ("unstemmed"))
  )
)[1]
```

Nothing really complex about that query – but playing around with it, I found that changing “unstemmed” to “stemmed” fixed it. I have no idea why an unstemmed query causes more trouble than a stemmed query which has much more work to do. Changing to a stemmed query wasn’t an option because that would limit the search to content in one language (see [this post][2] for more details on this weird behaviour).

Then the error was magically gone after a restart of the MarkLogic service. The classic ‘switch it off and on again’ fix. Although it’s a relief the problem is gone, it’s also really frustrating because it’s hard to carry on investigating the cause without being able to reproduce the error, and I just know it will come back again at some unknown point in the future. If I ever do get to the bottom of it I’ll post an update…

 [1]: http://www.google.co.uk/search?q=LISTCACHEFULL
 [2]: /2009/04/02/marklogic-searches-stemmed-vs-unstemmed.html