---
author: Rob
title: SyntaxHighlighter XQuery brush
excerpt:
layout: post
---

Update: Now hosted on GitHub:  
<http://github.com/robwhitby/SyntaxHighlighter-XQueryBrush>

I’ve just improved the code snippets in my posts by using the excellent [SyntaxHighlighter][1] by Alex Gorbatchev.

I had to write a new brush for XQuery, but this was pretty straightforward (it has a much better extension system than I found in Notepad++ for example). As well as XQuery 1.0 functions, keywords etc. I’ve included the MarkLogic 4.1 API.

Here’s an example..

```xqy
xquery version "1.0-ml";
declare variable $URI as xs:string external;

declare function local:document-move-forest(
  $uri as xs:string, 
  $forest-ids as xs:unsignedLong*
)
{
  xdmp:document-insert(
    $uri,
    fn:doc($uri),
    xdmp:document-get-permissions($uri),
    xdmp:document-get-collections($uri),
    xdmp:document-get-quality($uri),
    $forest-ids
  )
};

let $xml :=
  <xml att="blah" att2="blah">
    sdasd**asdasd**
  </xml>
```

If you want to use it download [SyntaxHighlighter][2], and then get the XQuery brush files from GitHub:  
<http://github.com/robwhitby/SyntaxHighlighter-XQueryBrush>

Example usage:

```html
<script type="text/javascript" src="scripts/shCore.js"></script>
<script type="text/javascript" src="scripts/shBrushXQuery.js"></script>
<link type="text/css" rel="stylesheet" href="styles/shCore.css"/>
<link type="text/css" rel="stylesheet" href="styles/shThemeDefault.css"/>
<link type="text/css" rel="stylesheet" href="styles/shThemeXQuery.css"/>
<script type="text/javascript">
	SyntaxHighlighter.config.clipboardSwf = 'scripts/clipboard.swf';
	SyntaxHighlighter.all();
</script>

<pre class="brush: xquery;">xquery version "1.0-ml";</pre>
```    

Next job is to change the layout of this blog to make the content column wider...

 [1]: http://alexgorbatchev.com/wiki/SyntaxHighlighter
 [2]: http://alexgorbatchev.com/wiki/SyntaxHighlighter:Download