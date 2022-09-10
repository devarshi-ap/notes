---
description: HTML
---

# Week 2

HTML documents consist of \<tags> which have:

* attributes - provide additional info about HTML elements (ie. class)



`<head>` - contains website metadata

`<title>` - tab title

`<body>` - site body content



#### Character Sets (charset)

* code that pairs each character from a given repertoire with a bit pattern. (ISO-8859-1, Windows-1252, UTF-8)

```markup
<meta charset="utf-8" />
```

#### Comments

* `<!-- This is a comment -->`

#### Colours

* represented by 6-digit hex value. (#RRGGBB)&#x20;
  * \#04f829: RR=04, GG=f8, BB=29
* Ranges from 00 (none) --> ff (max)

#### Text Formatting

* `<strong>` - bold
* `<em>` - italics
* `<code>` - monospace font (code effect)

#### Semantic Tags

* clearly self-describe (ie. article, header, footer, ...)
* almost all behave exactly like a div

#### Lists

* ul + li for bullet points
* ol + li for numbered bullets

#### Images

* 5 main supported types of images for the web: **GIF, PNG, JPG, WEPB, SVG**
* `<img>` - attributes:
  * src="cnTower.jpg"
  * alt="CN Tower"
  * (opt.) height="90%" (in px/%)
  * (opt.) width="12px" (in px/%)

#### Favicons

* small image displayed in tab title
* any image format can be used as a favicon, or a small **.ico** image can be created online at favicon.cc
* `<link rel-"icon" type="image/x-icon" href="path">`

#### Links & Anchors

* Relative:
  * `<a href="page.html">Click here</a>`
  * `<a href="../pages/page.html">Click here</a>`
* Absolute:
  * `<a href="https://www.espn.ca/">Click Here</a>`
* Internal:
  * `<a href="#top">Go to top</a>`
  * jumps to anchor tag: `<a name-"top">`

#### Meta Tag

* contains metadata about page such as:
  * **name** : name for metadata
  * **content** : value assc. w/ the name/http-equiv
  * **http-equiv** : http header for value of content attribute
  * **charset** : character set encoding

```markup
<!-- set page description ->
<meta name="description" content="Free Web tutorials on HTML, CSS, XML, and XHTML" />

<!-- set viewport to make page look good on all devices ->
<meta name="viewport" content="width=device-width, initial-scale=1.0" />

<!-- refresh page every 5s ->
<meta http-equiv="refresh" content="5" />
```

#### Form

* used to pass user data to a specified URL
* **action** : required attr for sending form data to server-side program.
* **method/name** : commonly used attr in forms
  * method="get" : sends form contents to URL
  * method="post" : sends form contents in the req body.



****
