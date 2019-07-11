---
title: "How to get the index of an iteration in a for-of loop in JavaScript"
date: 2018-11-07T07:00:00+02:00
description: ""
tags: js
---

A for-of loop, introduced in ES6, is a great way to iterate over an array:

```js
for (const v of ['a', 'b', 'c']) {
  console.log(v)
}
```

How can you get the index of an iteration?

The loop does not offer any syntax to do this, but you can combine the destructuring syntax introduced in [ES6](/es6/) with calling the `entries()` method on the array:

```js
for (const [i, v] of ['a', 'b', 'c'].entries()) {
  console.log(i, v)
}
```