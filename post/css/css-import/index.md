---
title: Importing a CSS file using @import
date: 2019-06-12T07:00:00+02:00
description: "Learn how to import CSS files using the @import directive"
tags: css
---

From any CSS file you can import another CSS file using the `@import` directive.

Here is how you use it:

```css
@import url(myfile.css)
```

url() can manage absolute or relative URLs.

One important thing you need to know is that `@import` directives must be put before any other CSS in the file, or they will be ignored.

You can use media descriptors to only load a CSS file on the specific media:

```css
@import url(myfile.css) all;
@import url(myfile-screen.css) screen;
@import url(myfile-print.css) print;
```