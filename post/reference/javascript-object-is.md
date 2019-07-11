---
title: "The Object is() method"
description: "Find out all about the JavaScript is() method of the Object object"
date: 2019-04-08T07:00:00+02:00
tags: js
---

This method was introduced in ES2015. It aims to help comparing values.

Usage:

```js
Object.is(a, b)
```

The result is always `false` unless:

- `a` and `b` are the same exact object
- `a` and `b` are equal strings (strings are equal when composed by the same characters, in the same order)
- `a` and `b` are equal numbers (numbers are equal when their value is equal)
- `a` and `b` are both `undefined`, both `null`, both `NaN`, both `true` or both `false`

`0` and `-0` are different values in JavaScript, so pay attention in this special case (convert all to `+0` using the `+` unary operator before comparing, for example).
