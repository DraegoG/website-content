---
title: call() and apply() in JavaScript
date: 2018-12-10T07:00:00+02:00
description: "Find out how to use call() and apply() and their difference in JavaScript"
tags: js
tags_weight: 26
---

call() and apply() are two functions that JavaScript offers to perform a very specific task: call a function and set its `this` value.

> Check out my ["this" guide](/javascript-this/) to know all the details about this particular variable

A function can use the `this` value for many different use cases. The problem is that it's given by the environment and cannot be changed from the outside, except when using `call()` or `apply()`.

When using those methods, you can pass in an additional object that will be used as `this` in the function invoked.

Those functions perform the same thing, but have a difference. In `call()` you can pass the function parameters as a comma separated list of parameters, taking as many parameters as you need, while in `apply()` you pass a single array that contains the parameters:

```js
const car = {
  brand: 'Ford',
  model: 'Fiesta'
}

const drive = function(from, to, kms) {
  console.log(`Driving for ${kms} kilometers from ${from} to ${to} with my car, a ${this.brand} ${this.model}`)
}

drive.call(car, 'Milan', 'Rome', 568)
drive.apply(car, ['Milan', 'Rome', 568])
```

Note that when using [arrow functions](/javascript-arrow-functions/) `this` is not bound, so this method only works with regular functions.