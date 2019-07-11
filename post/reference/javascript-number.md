---
title: "JavaScript Reference: Number"
description: "All about the JavaScript Number properties and methods"
date: 2019-03-26T07:00:00+02:00
tags: js
---

This article documents how to work with the `Number` built-in object, and lists its properties and methods.

A `number` value can be generated using a number literal syntax:

```js
const age = 36
typeof age //number
```

or using the `Number` global function:

```js
const age = Number(36)
typeof age //number
```

If we add the `new` keyword, we get a `Number` object in return:

```js
const age = new Number(36)
typeof age //object
```

which has a very different behavior than a `number` type. You can get the original `number` value using the `valueOf()` method:

```js
const age = new Number(36)
typeof age //object
age.valueOf() //36
```

## Properties

- `EPSILON` the smallest interval between two numbers
- `MAX_SAFE_INTEGER` the maximum integer value JavaScript can represent
- `MAX_VALUE` the maximum positive value JavaScript can represent
- `MIN_SAFE_INTEGER` the minimum integer value JavaScript can represent
- `MIN_VALUE` the minimum positive value JavaScript can represent
- `NaN` a special value representing "not a number"
- `NEGATIVE_INFINITY` a special value representing negative infinity
- `POSITIVE_INFINITY` a special value representing positive infinity

Those properties evaluated to the values listed below:

```js
Number.EPSILON
Number.MAX_SAFE_INTEGER
Number.MAX_VALUE
Number.MIN_SAFE_INTEGER
Number.MIN_VALUE
Number.NaN
Number.NEGATIVE_INFINITY
Number.POSITIVE_INFINITY
```

```js
2.220446049250313e-16
9007199254740991
1.7976931348623157e+308
-9007199254740991
5e-324
NaN
-Infinity
Infinity
```

## Object Methods

We can call those methods passing a value:

- [`Number.isNaN(value)`](/javascript-number-isnan/): returns true if `value` is not a number
- [`Number.isFinite(value)`](/javascript-number-isfinite/): returns true if `value` is a finite number
- [`Number.isInteger(value)`](/javascript-number-isinteger/): returns true if `value` is an integer
- [`Number.isSafeInteger(value)`](/javascript-number-issafeinteger/): returns true if `value` is a safe integer
- [`Number.parseFloat(value)`](/javascript-number-parsefloat/): converts `value` to a floating point number and returns it
- [`Number.parseInt(value)`](/javascript-number-parseint/): converts `value` to an integer and returns it

I mentioned "safe integer". Also up above, with the MAX_SAFE_INTEGER and MIN_SAFE_INTEGER properties. What is a safe integer? It's an integer that can be exactly represented as an IEEE-754 double precision number (all integers from (2^53 - 1) to -(2^53 - 1)). Out of this range, integers cannot be represented by JavaScript correctly. Out of the scope of the course, but [here is a great explanation of that](http://2ality.com/2013/10/safe-integers.html).

## Instance methods

When you use the `new` keyword to instantiate a value with the Number() function, we get a `Number` object in return:

```js
const age = new Number(36)
typeof age //object
```

This object offers a few unique methods you can use. Mostly to convert the number to specific formats.

- [`.toExponential()`](/javascript-number-toexponential/): return a string representing the number in exponential notation
- [`.toFixed()`](/javascript-number-tofixed/): return a string representing the number in fixed-point notation
- [`.toLocaleString()`](/javascript-number-tolocalestring/): return a string with the local specific conventions of the number
- [`.toPrecision()`](/javascript-number-toprecision/): return a string representing the number to a specified precision
- [`.toString()`](/javascript-number-tostring/): return a string representing the specified object in the specified radix (base). Overrides the Object.prototype.toString() method
- [`.valueOf()`](/javascript-number-valueof/): return the number primitive value of the object
