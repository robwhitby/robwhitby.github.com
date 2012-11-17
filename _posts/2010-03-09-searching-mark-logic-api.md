---
author: Rob
title: >
  Searching the MarkLogic API function
  reference with MarkLogic
excerpt:
layout: post
---

I’ve always thought it odd that the [MarkLogic API function reference][1] isn’t searchable. It seems obvious that it should be loaded into MarkLogic itself. Most of the time I use it for looking up the signature of a particular function, take [cts:uris()][2] for example – can anyone remember what order the parameters go in? Finding a function detail page from the home page is a mission, so I always just hit F3 to search the home page.

So anyway, I loaded the content into MarkLogic and built a quick interface using [ExtJS][3]. We’ve been using it at work for about 6 months, and it’s now got a new home at [api.xqueryhacker.com][4]. You can choose to search just function names or all content, and browse by namespace. There’s a link in the header to switch between version 4.0 and 4.1 of the API.

In the next few weeks I’ll tidy up the code and put it up on SourceForge so if anyone’s interested they can install it locally – I’m not really intending to publicly host it permanently.

As always, all feedback welcome..

[api.xqueryhacker.com][4]

 [1]: http://developer.marklogic.com/pubs/4.1/apidocs/All.html
 [2]: http://developer.marklogic.com/pubs/4.1/apidocs/Lexicons.html#cts:uris
 [3]: http://www.extjs.com
 [4]: http://api.xqueryhacker.com