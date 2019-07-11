---
title: How to get the value of a CSS property in JavaScript
date: 2019-07-07T07:00:00+02:00
description: "Say you want to fetch the value of a CSS property in a web page, one that is set using a stylesheet. How can you do so?"
tags: js
---

Say you want to fetch the value of a [CSS](/css/) property in a web page, one that is set using a stylesheet.

The `style` property of an element does not return it, because it only lists CSS properties defined in inline styles, or dynamically.

Not the properties defined in an external stylesheet.

So, how do you do it? Use `getComputedStyle()`, a global function:

```js
const element = document.querySelector('.my-element')
const style = getComputedStyle(element)
style.backgroundColor //the RGB value
```


