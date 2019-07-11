---
title: "The JavaScript Global Object"
date: 2019-06-21T07:06:15+02:00
description: "The details of the Global object in JavaScript"
tags: js
---

JavaScript provides a **global object** which has a set of properties, functions and objects that are accessed globally, without a namespace.

The properties are:

- `Infinity`
- `NaN`
- `undefined`

The functions are:

- `decodeURI()`
- `decodeURIComponent()`
- `encodeURI()`
- `encodeURIComponent()`
- `eval()`
- `isFinite()`
- `isNaN()`
- `parseFloat()`
- `parseInt()`

These are the objects:

- [`Array`](/javascript-array/)
- `Boolean`
- [`Date`](/javascript-dates/)
- `Function`
- [`JSON`](/json/)
- [`Math`](/javascript-math-object/)
- [`Number`](/javascript-number/)
- [`Object`](/javascript-object/)
- [`RegExp`](/javascript-regular-expressions/)
- [`String`](/javascript-string/)
- `Symbol`

and errors:

- `Error`
- `EvalError`
- `RangeError`
- `ReferenceError`
- `SyntaxError`
- `TypeError`
- `URIError`

I describe errors on this [JavaScript Errors reference](/javascript-errors/) post.

Let's now describe here the global properties and functions.

## `Infinity`

`Infinity` in JavaScript is a value that represents **infinity**.

Positive infinity. To get negative infinity, use the `–` operator: `-Infinity`.

Those are equivalent to `Number.POSITIVE_INFINITY` and `Number.NEGATIVE_INFINITY`.

Adding any number to `Infinity`, or multiplying `Infinity` for any number, still gives `Infinity`.

## `NaN`

The global `NaN` value is an acronym for `Not a Number`. It's returned by operations such as zero divided by zero, invalid parseInt() operations, or other operations.

```js
parseInt() //NaN
parseInt('a') //NaN
0/0 //NaN
```

A special thing to consider is that a `NaN` value is never equal to another `NaN` value. You must use the `isNaN()` global function to check if a value evaluates to `NaN`:

```js
NaN === NaN //false
0/0 === NaN //false
isNaN(0/0) //true
```

## `undefined`

The global `undefined` property holds the primitive value `undefined`.

Running a function that does not specify a return value returns `undefined`:

```js
const test = () => {}
test() //undefined
```

Unlike `NaN`, we can compare an `undefined` value with `undefined`, and get true:

```js
undefined === undefined
```

It's common to use the `typeof` operator to determine if a variable is undefined:

```js
if (typeof dog === 'undefined') {

}
```

## `decodeURI()`

Performs the opposite operation of `encodeURI()`

## `decodeURIComponent()`

Performs the opposite operation of `encodeURIComponent()`

## `encodeURI()`

This function is used to encode a complete URL. It does encode all characters to their HTML entities except the ones that have a special meaning in a URI structure, including all characters and digits, plus those special characters:

`~!@#$&*()=:/,;?+-_.`

Example:

```js
encodeURI("http://flaviocopes.com/ hey!/")
//"http://flaviocopes.com/%20hey!/"
```

## `encodeURIComponent()`

Similar to `encodeURI()`, `encodeURIComponent()` is meant to have a different job.

Instead of being used to encode an entire URI, it encodes a portion of a URI.

It does encode all characters to their HTML entities except the ones that have a special meaning in a URI structure, including all characters and digits, plus those special characters:

`-_.!~*'()`

Example:

```js
encodeURIComponent("http://www.example.org/a file with spaces.html")
// "http%3A%2F%2Fflaviocopes.com%2F%20hey!%2F"
```

## `eval()`

This is a special function that takes a string that contains JavaScript code, and evaluates / runs it.

This function is very rarely used and for a reason: it can be dangerous.

I recommend to read [this article](http://2ality.com/2014/01/eval.html) on the subject.

## `isFinite()`

Returns true if the value passed as parameter is finite.

```js
isFinite(1) //true
isFinite(Number.POSITIVE_INFINITY) //false
isFinite(Infinity) //false
```

## `isNaN()`

Returns true if the value passed as parameter evaluates to `NaN`.

```js
isNaN(NaN) //true
isNaN(Number.NaN) //true
isNaN('x') //true
isNaN(2) //false
isNaN(undefined) //true
```

This function is very useful because a `NaN` value is never equal to another `NaN` value. You must use the `isNaN()` global function to check if a value evaluates to `NaN`:

```js
0/0 === NaN //false
isNaN(0/0) //true
```

## `parseFloat()`

Like `parseInt()`, `parseFloat()` is used to convert a string value into a number, but retains the decimal part:

```js
parseFloat('10,000', 10) //10     ❌
parseFloat('10.00', 10) //10     ✅ (considered decimals, cut)
parseFloat('10.000', 10) //10     ✅ (considered decimals, cut)
parseFloat('10.20', 10) //10.2     ✅ (considered decimals)
parseFloat('10.81', 10) //10.81     ✅ (considered decimals)
parseFloat('10000', 10) //10000  ✅
```

## `parseInt()`

This function is used to convert a string value into a number.

Another good solution for integers is to call the `parseInt()` function:

```js
const count = parseInt('1234', 10) //1234
```

Don't forget the second parameter, which is the radix, always 10 for decimal numbers, or the conversion might try to guess the radix and give unexpected results.

`parseInt()` tries to get a number from a string that does not only contain a number:

```js
parseInt('10 lions', 10) //10
```

but if the string does not start with a number, you'll get `NaN` (Not a Number):

```js
parseInt("I'm 10", 10) //NaN
```

Also, just like Number it's not reliable with separators between the digits:

```js
parseInt('10,000', 10) //10     ❌
parseInt('10.00', 10) //10     ✅ (considered decimals, cut)
parseInt('10.000', 10) //10     ✅ (considered decimals, cut)
parseInt('10.20', 10) //10     ✅ (considered decimals, cut)
parseInt('10.81', 10) //10     ✅ (considered decimals, cut)
parseInt('10000', 10) //10000  ✅
```
