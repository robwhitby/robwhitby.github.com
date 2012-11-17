---
author: Rob
title: 'MarkLogic XQuery performance tuning - computing facets concurrently'
excerpt:
layout: post
---

As seems to be quite common in search applications built on MarkLogic, our latest project has a lot of facets, varying from document language with only a handful of values to publication title with over 50,000. Facets are very fast to calculate, but with a lot of distinct values in each facet, it can easily take a couple of tenths of a second per facet. With multiple facets the time really starts adding up. Profiling our search queries revealed that over 70% of the time was taken up with faceting.

The code looked something like this. The facets are defined in XML and there is a function to resolve a single facet which is called on each using function mapping. The total time was around 0.5 seconds.

<script src="https://gist.github.com/1556015.js?file=cts-element-values-non-concurrent.xqy"></script>

The `cts:element-values` function has an option called ‘concurrent’. The description from the [API documentation][1]:

> Perform the work concurrently in another thread. This is a hint to the query optimizer to help parallelize the lexicon work, allowing the calling query to continue performing other work while the lexicon processing occurs. This is especially useful in cases where multiple lexicon calls occur in the same query (for example, resolving many facets in a single query).

Unfortunately simply adding the concurrent option to the facet definitions doesn’t make any difference because the function mapping is blocked waiting for the response of each call. The same would happen if we looped over the facets in a FLWOR statement. 

One solution is to rewrite the resolve-facet function to recurse through the facets, only accessing the results of cts:element-values after the recursive call. This way it will loop through the entire sequence of facets first and the expensive calls won’t be blocked. Total time is now 0.2 seconds – the time of the slowest facet.

<script src="https://gist.github.com/1555988.js?file=cts-element-values-concurrent.xqy"></script>


By the way, if you’re using the MarkLogic search API then there’s no need to do anything, it already computes facets concurrently – sorry for wasting your time :) 

It’s also worth noting that this technique isn’t limited to cts:element-values, other lexicon functions also support the concurrent option.

 [1]: http://api.xqueryhacker.com/#cts:element-values