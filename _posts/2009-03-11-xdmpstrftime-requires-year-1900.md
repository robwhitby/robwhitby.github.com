---
author: Rob
title: 'xdmp:strftime() requires year &gt;= 1900'
excerpt: 'There’s a weird bug in the xdmp:strftime() function'
layout: post
tags: 
  - XQuery
  - MarkLogic
---
There’s a weird bug in the `xdmp:strftime()` function in MarkLogic, I  
think inherited from elsewhere, that causes an error when supplied a year less than 1900.

```xqy
xdmp:strftime('%Y', xs:dateTime("1890-01-01T00:00:00"))
```

    SVC-STRFTIMEYEAR: xdmp:strftime(“%Y”, xs:dateTime(“1890-01-01T00:00:00″)) 
    — Year cannot be formatted: 1890

As a work-around call this function in a custom namespace:

```xqy
define function strftime($format as xs:string, $dt as xs:dateTime)
as xs:string
{
  fn:replace(
    xdmp:strftime(fn:replace($format, "%Y", "#Y"), $dt),
    '#Y',
    fn:string(fn:year-from-date(xs:date($dt)))
  )
}
```