---
author: Rob
title: Some ideas for MarkLogic enhancements
excerpt:
layout: post
---

A random assortment of ideas for MarkLogic v next. Some big, some small.


## Improve logging

All log messages go into ErrorLog.txt, and there's one per host so finding anything in a cluster is a pain. The access logs are the same and their format is fixed. How about..

* Multiple custom log files, with configuration options per app server. e.g. enable DEBUG for app server A writing to /logs/my-logfile.txt.

* Configurable format for the fields in access logs.

* Support sending logs to external aggregators


## Embrace distribution

The MarkLogic binaries are not allowed to be redistributed ([eula][eula]). You have to have an account to download. This is a massive barrier to developer adoption. Imagine if developers new to MarkLogic could run one command to get a working instance up and running locally. No signing up for the developer site, no entering a licence, nothing to get in the way of trying out the software.

`brew/yum install marklogic`

Or even better, be able to pull a docker image from [docker hub][dockerhub]. Encourage people to distribute docker images with applications and even data pre-installed.


## Support UDP

Provide a way of sending UDP messages from XQuery. There's lots of metrics and tracing tools that it would be great to integrate with. e.g. [statsd][statsd] and [zipkin][zipkin].


## Open up access to the system

Execute shell commands from within XQuery.

`xdmp:exec("ls")`

(but see function namespacing below..)


## Custom tokenization

Why just for fields? This should be available at the database level (see below).


## Simplify database configuration

This is a big one, but something has to be done to get configuration under control. It applies to everything really, but database config is probably the biggest cause of confusion I see. There's overlapping config at the db level, element level, separate word query config, fields, fragments, word lexicons. Figuring out how all these interact with each other and their impact on search is nigh on impossible.

Part of this is about improving documentation and UI in the admin interface, but mainly it's about rationalising the options.


## Automate cluster configuration

Wouldn't it be great if you could specify that you want a new database, and the data should be replicated to *n* other hosts, and MarkLogic just did it. No mention of master and replica forests or failover config. Ideally just tell MarkLogic upfront where your data should be stored and it manages everything from then on - creating the forests, replicas, balancing data, adapting when adding/removing hosts etc.


## Function namespacing

Namespaces! Why aren't functions grouped into sensible namespaces? Most functions are just lumped into xdmp. There are currently 472 functions that do wildly different things like `xdmp:add-response-header`, `xdmp:email`, `xdmp:x509-certificate-extract`, `xdmp:xslt-invoke`, `xdmp:start-journal-archiving`.


## Computed indexes

This is an [old idea][oldpost] I still like.


## Support the latest specs

There's lots of nice updates in XQuery/XPath 3.1. The new [maps and arrays][xqy31] would make a massive difference as well as sugar like the [arrow operator][xpath31].


## Be more open

Finally, how about opening up the product roadmap and RFEs? Allow discussion and even voting on new features. The same applies to bugs - don't be shy, open up the bug tracker.


[zipkin]: http://twitter.github.io/zipkin/
[statsd]: https://github.com/etsy/statsd/
[oldpost]: http://www.xqueryhacker.com/2012/03/03/computed-indexes-in-marklogic.html
[xpath31]: http://www.w3.org/TR/xpath-31/#id-arrow-operator
[xqy31]: http://www.w3.org/TR/xquery-31/#id-revision-log
[eula]: http://developer.marklogic.com/eula
[dockerhub]: http://hub.docker.com
