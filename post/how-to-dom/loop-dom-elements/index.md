---
title: How to loop over DOM elements from querySelectorAll
description: "TL;DR: Use the for..of loop"
date: 2018-10-19T07:00:00+02:00
tags: browser
---

The `querySelectorAll()` method run on `document` returns a list of DOM elements that satisfy the selectors query.

It returns a list of elements, which is not an array but a [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) object.

The easiest way to loop over the results is to use the `for..of` loop:

```js
for (const item of document.querySelectorAll('.buttons')) {
  //...do something
}
```
