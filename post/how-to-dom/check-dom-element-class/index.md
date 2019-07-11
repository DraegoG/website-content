---
title: How to check if a DOM element has a class
description: "How do you check if a particular DOM element you have the reference of, has a class?"
date: 2018-10-22T07:00:00+02:00
tags: browser
---

Use the `contains` method provided by the `classList` object, which is:

```js
element.classList.contains('myclass')
```

Technically, classList is an object that satisfies the `DOMTokenList` interface, which means it implements its methods and properties.

You can see its details on [the DOMTokenList MDN page](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList).
