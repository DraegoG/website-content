---
title: How to change a DOM node value
description: "Given a DOM element, how do you change its value?"
date: 2018-10-23T07:00:00+02:00
tags: browser
---

Change the value of the `innerText` property:

```js
element.innerText = 'x'
```

To lookup the element, combine it with the [Selectors API](https://flaviocopes.com/selectors-api/):

```js
document.querySelector('#today .total')
```