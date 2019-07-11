---
title: "The Number isSafeInteger() method"
description: "Find out all about the JavaScript isSafeInteger() method of the Number object"
date: 2019-03-16T07:00:00+02:00
tags: js
---

A number might satisfy [`Number.isInteger()`](/javascript-number-isinteger/) but not  `Number.isSafeInteger()` if it goes out of the boundaries of safe integers, which I explained above.

So, anything over `2^53` and below `-2^53` is not safe:

```js
Number.isSafeInteger(Math.pow(2, 53)) // false
Number.isSafeInteger(Math.pow(2, 53) - 1) // true
Number.isSafeInteger(Math.pow(2, 53) + 1) // false
Number.isSafeInteger(-Math.pow(2, 53)) // false
Number.isSafeInteger(-Math.pow(2, 53) - 1) // false
Number.isSafeInteger(-Math.pow(2, 53) + 1) // true
```
