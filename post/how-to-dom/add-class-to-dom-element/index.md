---
title: How to add a class to a DOM element
description: "TL;DR: Use the add() method on element.classList"
date: 2018-10-18T07:00:00+02:00
tags: browser
---

When you have a DOM element reference you can add a new class to it by using the `add` method:

```js
element.classList.add('myclass')
```

You can remove a class using the `remove` method:

```js
element.classList.remove('myclass')
```

Implementation detail: `classList` is not an array, but rather it is a collection of type [DOMTokenList](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList).

You can't directly edit `classList` because it's a read-only property. You can however use its methods to change the element classes.