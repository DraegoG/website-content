---
title: JavaScript Equality Operators
date: 2019-05-31T07:00:00+02:00
description: "Learn the basics of the JavaScript Equality Operators"
tags: js
---

Those operators accept two values and return a boolean:

- `==` checks for equality
- `!=` checks for inequality
- `===` checks for strict equality
- `!==` checks for strict inequality

Let's talk what we mean for _strict_. Without the strict check, the second operand is converted to the type of the first before making the comparison. Strict prevents this.

Examples:

```js
const a = true

a == true //true
a === true //true

1 == 1 //true
1 == '1' //true
1 === 1 //true
1 === '1' //false
```

You cannot check objects for equality: two objects are never equal to each other. The only case when a check might be true is if two variables reference the same object.

Some peculiarities to be aware: `NaN` is always different from `NaN`.

```js
NaN == NaN //false
```

`null` and `undefined` values are equal if compared in non-strict mode:

```js
null == undefined //true
null === undefined //false
```
