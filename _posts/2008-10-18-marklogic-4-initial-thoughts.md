---
author: Rob
title: MarkLogic 4 - Initial thoughts
excerpt: Last week I upgraded our development server to MarkLogic 4.0.1. The actual installation process ...
layout: post
tags: 
  - XQuery
  - MarkLogic
---

Last week I upgraded our development server to MarkLogic 4.0.1. The actual installation process was pretty simple – uninstall 3, install 4. Thankfully it kept all the databases, app servers and configuration. The only delay was reindexing the content, which took about 4 days for a 160gb database (3.3m fragments). 

ML 4 now supports XQuery 1.0, but automatically sets existing app servers to use 0.9 to maintain compatibility. There were still a number of small code changes I had to make to get our apps running, seemingly because even in 0.9 mode it is still stricter with parsing/executing xquery code:

*   I had an xquery file which imported a module which i wasn’t actually using, and it had a syntax error in it. In 3.2 this didn’t cause any problems but in 4.0 it threw an exception. Makes sense, and it’s my fault I know but it’s a difference none the less..
*   Another issue arguably caused by my slack programming… When specifying the return type of a function, if the function actually returns a different type ML 4.0 now enforces a conversion to the type specified. e.g.

{% highlight xqy %}
declare function get-title() as xs:string {
    <title>the <b>title</b></title>
};
<x>{getTitle()}</x>
{% endhighlight %}    

returns..

ML 3.2.8: `<x><title>the  <b>title</b></title></x>`  
ML 4.0.1: `<x>the title</x>` 

No argument, ML 4 has it right, but it did break my app and took a while to figure out.

ML 4 has some interesting new features – XQuery 1.0, the geospacial stuff looks cool, and the forest level failover is something we’re going to use straight away. I was a bit disappointed they didn’t take the chance to address some other areas:

*   Still no integrated XSLT engine. Come on guys, just admit XQuery isn’t great at everything!
*   Indexes are still specified by QName.  It would be great to specify a path, so i can put an index on /article/author, to prevent it also indexing /article/reference/author
*   Registered queries are still too much of a pain to bother with. I mean – you have to call them by an id number and they don’t persist after a restart, so every time you call it you have to check it exists… pah.
*   Error messages. Still awful.