---
author: Rob
title: MarkLogic improvements
excerpt: I was recently asked to write a list of improvements I’d like to see in ...
layout: post
tags: 
  - XQuery
  - MarkLogic
---
I was recently asked to write a list of improvements I’d like to see in future MarkLogic releases – here’s what I came up with:

**Server**

*   Error messages are sometimes misleading and unhelpful
*   Logging restricted to global errorLog.txt
*   Can’t index an element at a specific XPath (can only specify QName which is often not unique)
*   Registered queries are too much effort to use – they don’t persist after restart and have to be called by id
*   Stemmed/Unstemmed queries search different content base because stemmed searches are single language
*   XML update functions (eg xdmp:node-replace) don’t work on in-memory nodes
*   No built-in XSLT engine
*   Ease of scalability by adding ‘commodity hardware’ undermined by licensing model per CPU

  
**Admin site**

*   Hard to navigate – tree structure confusing
*   Limited help – just loads of text fields with no hints to valid settings
*   Times out when the server has a problem.
*   API docs aren’t searchable (why not index in MarkLogic?!)

  
**Developer Tools (e.g. Record Loader, CQ, Corb, lib-search)**

*   Suffer from not being official products – very limited support, erratic development
*   In general they are not robust, are poorly designed, hard to set up and use (e.g. CQ UI is very basic, record loader leaks memory)
*   All poorly documented
*   Common development requirements not catered for. e.g. import/export server configuration
*   Mailing list is only help availalble – would be nice to have forums and online tutorials
*   XCC – .Net version is just a wrapper around Java so incurs performance penalty

I should point out that I really like working with MarkLogic, and it’s easy to take for granted what a powerful piece of software it is. Most of my gripes concern the tools and documentation that support it. I feel they’ve been neglected so far which is a shame but I guess understandable for a new and quickly evolving product.