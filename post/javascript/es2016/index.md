---
title: The ES2016 Guide
description: "ECMAScript is the standard upon which JavaScript is based, and it's often abbreviated to ES. Discover everything about ECMAScript, and the features added in ES2016, aka ES7"
date: 2018-10-01T15:00:00+02:00
tags: js
tags_weight: 3
---

<!-- TOC -->

- [Array.prototype.includes()](#arrayprototypeincludes)
- [Exponentiation Operator](#exponentiation-operator)

<!-- /TOC -->

ES2016, officially known as ECMAScript 2016, was finalized in June 2016.

Compared to ES2015, ES2016 is a tiny release for JavaScript, containing just two features:

- Array.prototype.includes
- Exponentiation Operator

## Array.prototype.includes()

This feature introduces a more readable syntax for checking if an array contains an element.

With ES6 and lower, to check if an array contained an element you had to use `indexOf`, which checks the index in the array, and returns `-1` if the element is not there.

Since `-1` is evaluated as a true value, you could **not** do for example

```js
if (![1,2].indexOf(3)) {
  console.log('Not found')
}
```

With this feature introduced in ES2016 we can do

```js
if (![1,2].includes(3)) {
  console.log('Not found')
}
```

## Exponentiation Operator

The exponentiation operator `**` is the equivalent of `Math.pow()`, but brought into the language instead of being a library function.

```js
Math.pow(4, 2) == 4 ** 2
```

This feature is a nice addition for math intensive JS applications.

The `**` operator is standardized across many languages including Python, Ruby, MATLAB, Lua, Perl and many others.
