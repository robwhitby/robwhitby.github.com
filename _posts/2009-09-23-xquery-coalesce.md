---
author: Rob
title: XQuery coalesce
excerpt:
layout: post
---

A little trick I picked up recently..

XQuery doesn’t have a coalesce function so I was writing code like:

```xqy
if ($x) then $x else "default value"
````

But there’s a nicer way which shows why there’s no need for a coalesce function:

```xqy
($x, "default value")[1]
```
Everything is a sequence…