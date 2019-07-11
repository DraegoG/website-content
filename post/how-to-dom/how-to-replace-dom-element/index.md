---
title: How to replace a DOM element
description: "Given a DOM element, how do you replace it with another?"
date: 2018-12-02T07:00:00+02:00
tags: browser
---

Say you have a DOM element, which you have a reference to (maybe retrieved using [`querySelector()`](https://flaviocopes.com/selectors-api/)).

To replace it with another DOM element, you can call the `replaceWith()` method on the first element, passing the second element as argument:

```js
const el1 = document.querySelector(/* ... */)
const el2 = document.querySelector(/* ... */)

el1.replaceWith(el2)
```

Since Edge <17 and IE11 [do not support it](https://caniuse.com/#feat=dom-manip-convenience), you should transpile it to ES5 using Babel if you plan to support those browsers.

Another solution is to lookup the parent and use the `replaceChild()` method, which is much older and supported by all browsers:

```js
const el1 = document.querySelector(/* ... */)
const el2 = document.querySelector(/* ... */)

el1.parentNode.replaceChild(el2, el1)
```