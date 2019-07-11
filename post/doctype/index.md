---
title: "What is the Doctype"
description: "Any HTML document must start with a Document Type Declaration, abbreviated Doctype, which tells the browser the version of HTML used in the page"
date: 2018-04-20T07:06:29+02:00
booktitle: The Doctype
tags: browser
---

Any HTML document must start with a _Document Type Declaration_ (abbreviated **doctype**) in the first line, which tells the browser the version of HTML used in the page.

This doctype declaration (case insensitive):

```html
<!DOCTYPE html>
```

tells the browser this is an **HTML5 document**.

## Browser rendering mode

With this declaration, the browser can render the document in **standards mode**.

Without it, browsers render the page in **quirks mode**.

If you've never heard of quirks mode, you must know that browsers introduced this rendering mode to make pages written in an "old style" compatible with new functionality and standards used. Without it, as browsers and HTML evolved, old pages would break their appearance, and the Web Platform has historically been very protective in this regard (which I think is part of its success).

Browsers basically default to quirks mode unless they recognize the page is written for standards mode.

**You want standards mode**, and

```html
<!DOCTYPE html>
```

is the way to get it.

There's an additional care to be put for Internet Explorer <= 10 users to avoid quirks mode, and it's to put

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

in the page `<head>` tag, before loading any script.

## Older HTML versions

HTML has a weird set of versions:

- HTML (1991)
- HTML 2.0 (1995)
- HTML 3.2 (1997)
- HTML 4.01 (1999)
- XHTML (2000)
- HTML5 (2014)

The doctype of an HTML 4.01 Strict document was:

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
  "http://www.w3.org/TR/html4/strict.dtd">
```

XHTML was similar:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

They required a DTD (_Document Type Definition_) because those old HTML versions were based on SGML, a format that defines the structure of a document.

XHTML also required the `html` tag to have a namespace, like this:

```html
<html xmlns="http://www.w3.org/1999/xhtml">
```

Those doctype declarations always required you to save the DTD declaration somewhere, as it's nearly impossible to memorize. Also, there were different DTDs for strict mode or transitional mode (which was less strict).

XHTML is an XML vocabulary, while HTML4 (and lower) is an SGML application. The current HTML, HTML5, is heavily inspired by HTML4, but is not an SGML application, and abandoned many of the strict rules of XHTML.

HTML5 is not based on SGML, but on its own standard, so the DTD is not required, and we benefit from this in this very simple declaration:

```html
<!DOCTYPE html>
```