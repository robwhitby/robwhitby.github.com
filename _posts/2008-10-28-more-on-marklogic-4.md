---
author: Rob
title: More on MarkLogic 4
excerpt: Just remembered another feature that I’d really like to see in MarkLogic...
layout: post
tags: 
  - XQuery
  - MarkLogic
---

Just remembered another feature that I’d really like to see in MarkLogic.. the admin interface currently shows the size of a database in mb. It would be useful to break that into data size and index sizes. If I add an index I’d like to know how much space it takes up, and also whether it is fully loaded into RAM or not.

On the topic of indexes, it’s hard to nail down which functions (eg cts:element-query)  make use of which indexes. Ideally there would be a more consistent naming convention of indexes and functions to make it more obvious, but an easier solution would be to simply add information to the function reference – so for each function some detail on which indexes will be used if available.