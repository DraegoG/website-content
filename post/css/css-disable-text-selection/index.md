---
title: "How to disable text selection using CSS"
date: 2019-07-30T07:00:00+02:00
description: "Find out how to disable text selection using the CSS property `user-select`"
tags: css
---

By default browsers let us select the text in the browser using the keyboard, pressing the cmd-A combination on a Mac for example, or using the mouse.

How can you disable that, to make your web page behave more like an app and less like a document?

Use the `user-select: none;` CSS rule.

You need to use browser prefixes, as [https://caniuse.com/#feat=user-select-none](https://caniuse.com/#feat=user-select-none) tells us:

```css
-webkit-touch-callout: none;
  -webkit-user-select: none;
   -khtml-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
```

One thing I use sometimes is to make all the app interface unselectable applying `user-select: none;` on the body element, then I can re-enable it on specific elements, using:

```css
user-select: text;
```
