---
author: Rob
title: Format number in XQuery
excerpt:
layout: post
---

I may be blind and all this was for nothing, but I couldn’t find an easy way to format a number with thousand separators – e.g. 1,234.

So I wrote this little function:

{% highlight xqy %}
declare function local:format-int($i as xs:int) as xs:string
{
  let $input :=
    if ($i lt 0) then fn:substring(fn:string($i), 2)
    else fn:string($i)
  let $rev := fn:reverse(fn:string-to-codepoints(fn:string($input)))
  let $comma := fn:string-to-codepoints(',')

  let $chars :=
    for $c at $i in $rev
    return (
      $c,
      if ($i mod 3 eq 0 and fn:not($i eq count($rev)))
      then $comma else ()
    )

  return fn:concat(
    if ($i lt 0) then '-' else (),
    fn:codepoints-to-string(fn:reverse($chars))
  )
};
{% endhighlight %}

tests:

{% highlight xqy %}
local:format-int((1, 12, 123, 1234, 12345, 123456, 1234567,
    123456789, 1234567890, -12, -12345, -1234567))
{% endhighlight %}

(By the way, I think that’s the first time I’ve found a use for function mapping)

I guess I could go further and support different format specifications, and doubles etc., but for now this is all I need. And I’m suspicious that it’s just existing functionality I can’t find… any pointers welcome!