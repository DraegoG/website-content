---
title: "How to check if a JavaScript object property is undefined"
date: 2018-05-26T07:06:15+02:00
updated: 2019-05-29T07:06:15+02:00
description: "In a JavaScript program, the correct way to check if an object property is undefined is to use the `typeof` operator. See how you can use it with this simple explanation"
tags: js
so: true
---

In a JavaScript program, the correct way to check if an object property is undefined is to use the `typeof` operator.

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/NUj3yePDlFk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

`typeof` returns a string that tells the type of the operand. It is used without parentheses, passing it any value you want to check:

```js
const list = []
const count = 2

typeof list //"object"
typeof count //"number"
typeof "test" //"string"

typeof color //"undefined"
```

If the value is not defined, `typeof` returns the 'undefined' **string**.

Now suppose you have a `car` object, with just one property:

```js
const car = {
  model: 'Fiesta'
}
```

This is how you check if the `color` property is defined on this object:

```js
if (typeof car.color === 'undefined') {
  // color is undefined
}
```

