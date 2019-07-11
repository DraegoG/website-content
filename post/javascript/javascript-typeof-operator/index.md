---
title: JavaScript typeof Operator
date: 2019-05-01T07:00:00+02:00
description: "Learn the basics of the JavaScript typeof Operator"
tags: js
---

In JavaScript, any value has a type assigned.

The `typeof` operator is a unary operator that returns a string representing the type of a variable.

Example usage:

```js
typeof 1 //'number'
typeof '1' //'string'
typeof {name: 'Flavio'} //'object'
typeof [1, 2, 3] //'object'
typeof true //'boolean'
typeof undefined //'undefined'
typeof (() => {}) //'function'
typeof Symbol() //'symbol'
```

JavaScript has no "function" type, and it seems funny that `typeof` returns `'function'` when we pass it a function.

It's one quirk of it, to make our job easier.

If you don't initialize the variable when you declare it, it will have the `undefined` value until you assign a value to it.

```js
let a //typeof a === 'undefined'
```

`typeof` works also on object properties.

If you have a `car` object, with just one property:

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