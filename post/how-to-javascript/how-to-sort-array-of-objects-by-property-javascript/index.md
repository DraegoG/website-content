---
title: How to sort an array of objects by a property value in JavaScript
date: 2018-12-06T07:00:00+02:00
updated: 2019-06-06T07:00:00+02:00
description: "Find out how to sort an array of objects by a property value in JavaScript"
tags: js
---

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/qy8TcQSGuoI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

Say you have an array of objects like this:

```js
const list = [
  { color: 'white', size: 'XXL' },
  { color: 'red', size: 'XL' },
  { color: 'black', size: 'M' }
]
```

You want to render this list, but first you want to order it by the value of one of the properties. For example you want to order it by the color name, in alphabetical order: black, red, white.

You can use the `sort()` method of `Array`, which takes a callback function, which takes as parameters 2 objects contained in the array (which we call `a` and `b`):

```js
list.sort((a, b) => (a.color > b.color) ? 1 : -1)
```

When we return 1, the function communicates to `sort()` that the object `b` takes precedence in sorting over the object `a`. Returning `-1` would do the opposite.

The callback function could calculate other properties too, to handle the case where the color is the same, and order by a secondary property as well:

```js
list.sort((a, b) => (a.color > b.color) ? 1 : (a.color === b.color) ? ((a.size > b.size) ? 1 : -1) : -1 )
```
