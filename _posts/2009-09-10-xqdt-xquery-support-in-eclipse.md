---
author: Rob
title: 'XQDT - XQuery support in Eclipse'
excerpt:
layout: post
---

I’ve found a new project that adds XQuery support to [Eclipse][1] – [XQDT][2].

It’s early days for the plugin but already it looks very good. It has proper syntax highlighting, live code validation, auto-complete and crucially can connect to MarkLogic to execute the query within Eclipse. It looks like it validates code as XQuery 1.1 – so anything written in 0.9 will show false errors. Don’t think this will cause problems with 1.0-ml though, and it recognises the MarkLogic API functions.

I recommend giving it a try – I’ve already switched from Notepad++ and so far so good.

 [1]: http://www.eclipse.org/
 [2]: http://www.xqdt.org