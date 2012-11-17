---
author: Rob
title: MarkLogic to add XSLT 2.0 support
excerpt:
layout: post
---

Good news! [MarkLogic][1] has been listening to it’s customers and are working on adding XSLT 2.0 support. [Norman Walsh][2] announced the news at a MarkLogic user group meeting in New York – see his [blog post][3] for details. In the past the argument has always been XSLT is unnecessary because XQuery is enough, so it’s nice to see acceptance that XQuery isn’t the best tool for every job.

I can see this being of great benefit at our company where we have far more experience with XSLT compared to XQuery. The separation of query and output will allow us to write cleaner, more focussed XQueries and leave the specifics of different output formats to XSLT. This should make debugging and performance tuning XQuery much simpler.

Only downside is we can’t start using it straight away, and as yet there’s no information on when it will be released.

 [1]: http://www.marklogic.com
 [2]: http://norman.walsh.name
 [3]: http://norman.walsh.name/2009/11/12/nymug