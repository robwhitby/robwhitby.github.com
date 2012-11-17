---
author: Rob
title: "Early version of DQ - an alternative interface for Mark Logic's CQ XQuery editor"
excerpt:
layout: post
---

Update: The project has now moved to github.  
<http://github.com/robwhitby/DQ>

[DQ v0.2 now available][1]

Here’s a very early version of a new interface to [CQ][2] that I’m slowly working on, imaginatively named [DQ][3]. It aims to address a number of shortcomings in CQ, the web XQuery interface provided by [Mark Logic][4].

**Current features**  
Tabbed code editor (based on [EditArea][5]) with XQuery syntax highlighting, search and replace, and support of tab key  
Save queries and results to file system  
Auto-save of all query tabs using browser local storage (no more session confusion)  
Highlighting a section of code and executing will run just the selected code (inspired by SQL Query Analyzer!)

**Future features**  
Integration of XQuery API reference  
Function auto-complete  
More suggestions welcome!

**Requirements**  
Recent version of [CQ][2] installed (I’m using 4.1.2)  
Firefox 3.5 or IE8 (Chrome doesn’t style XML output, Safari and Opera not yet tested)

**Installation**  
Unzip DQ folder in root of your CQ directory  
Browse to: http://SERVER:CQPORT/DQ

The project is up on sourceforge:  
<https://sourceforge.net/projects/mldq/>

Please give it a go and let me know what you think. I’d be interested in suggestions on improvements, extra features etc.

 [1]: /2011/03/15/dq-update-marklogic-cq.html
 [2]: http://developer.marklogic.com/code/
 [3]: https://sourceforge.net/projects/mldq/
 [4]: http://www.marklogic.com
 [5]: https://sourceforge.net/projects/editarea/