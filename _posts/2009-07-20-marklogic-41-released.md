---
author: Rob
title: MarkLogic 4.1 Released
excerpt:
layout: post
---

[MarkLogic ][1]have released version 4.1, not long after 4.0 came out. I haven’t had a chance to use it yet but it looks like there are a few cool new features:

*   XML schema validation
*   Japanese language support
*   Task scheduler
*   JSON support
*   HTTP app servers supports REST, URL rewriting and HTTPS
*   MarkLogic Application Services – includes a new search API that seems to  
    be a move to provide built-in functionality like lib-search, and a GUI  
    tool to develop demos. 

The JSON support would have been really valuable in the project I just finished, and I can see how useful a task scheduler would be for maintenance jobs etc. The improvements to the HTTP app server don’t really interest me. Why would you want to use MarkLogic as an HTTP server in any real production environment? Despite these improvements, it’s woefully under-featured compared to Apache or IIS, and is an expensive MarkLogic cluster really the right place to be handling HTTP requests?

And as for the application builder GUI… I haven’t checked it out just, but the idea scares me to death. I can just imagine people knocking something up that nearly works and then thinking creating a proper, scalable, production-ready application should be just as quick and easy.

Now just need to find a way to justify upgrading our cluster – doubt it will happen any time soon unfortunately..

 [1]: http://www.marklogic.com/