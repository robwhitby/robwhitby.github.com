---
author: Rob
title: AuthorMapper.com
excerpt: My first big project with MarkLogic went live about a month back
layout: post
tags: 
  - XQuery
  - MarkLogic
  - AuthorMapper
  - ExtJS
---
My first big project with MarkLogic went live about a month back: [AuthorMapper][1].

We loaded all [Springer][2] journal content (3m+ articles) into [MarkLogic][3] and used lib-search as a basis for a faceted search interface. Using [Google’s geocoding service][4] we store the long/lat coordinates of the authors enabling plotting the results on the Google map. The JavaScript framework [Ext JS][5] is used for the search form and some other nice UI tweaks like resizing the map.


 [1]: http://www.authormapper.com
 [2]: http://www.springer.com
 [3]: http://www.marklogic.com
 [4]: http://code.google.com/apis/maps/documentation/geocoding/index.html
 [5]: http://extjs.com