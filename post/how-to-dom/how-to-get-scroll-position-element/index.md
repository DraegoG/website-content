---
title: "How to get the scroll position of an element in JavaScript"
date: 2018-12-01T07:00:00+02:00
description: "When you are building a user interface in the browser, you might have an element which can be scrolled, and it's a common need to know the horizontal and vertical scrolling it currently has."
tags: browser
---

How can you do that?

Once you have the element, you can inspect its  `scrollLeft` and `scrollTop` properties.

The `0, 0` position is always found in the top left corner, so any scrolling is relative to that.

Example:

```js
const container = document.querySelector('. container')
container.scrollTop
container.scrollLeft
```

Those properties are read/write, so you can also **set** the scroll position:

```js
const container = document.querySelector('. container')
container.scrollTop = 1000
container.scrollLeft = 1000
```

![](Screen Shot 2018-11-09 at 15.50.57.png)