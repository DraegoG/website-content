---
title: "The JavaScript Arithmetic operators"
description: "Performing math operations and calculus is a very common thing to do with any programming language. JavaScript offers several operators to help us work with numbers"
date: 2018-07-17T07:06:29+02:00
updated: 2019-04-27T07:06:29+02:00
tags: js
---

Performing math operations and calculus is a very common thing to do with any programming language.

JavaScript offers several operators to help us work with numbers.

- [Addition (+)](#addition)
- [Subtraction (-)](#subtraction)
- [Division (/)](#division)
- [Remainder (%)](#remainder)
- [Multiplication (*)](#multiplication)
- [Exponentiation (**)](#exponentiation)
- [Increment (++)](#increment)
- [Decrement (`--`)](#decrement)
- [Unary negation (-)](#unary-negation)
- [Unary plus (+)](#unary-plus)

## Addition (+)

```js
const three = 1 + 2
const four = three + 1
```

The `+` operator also serves as string concatenation if you use strings, so pay attention:

```js
const three = 1 + 2
three + 1 // 4
'three' + 1 // three1
```

## Subtraction (-)

```js
const two = 4 - 2
```

## Division (/)

Returns the quotient of the first operator and the second:

```js
const result = 20 / 5 //result === 4
const result = 20 / 7 //result === 2.857142857142857
```

If you divide by zero, JavaScript does not raise any error but returns the `Infinity` value (or `-Infinity` if the value is negative).

```js
1 / 0 //Infinity
-1 / 0 //-Infinity
```

## Remainder (%)

The remainder is a very useful calculation in many use cases:

```js
const result = 20 % 5 //result === 0
const result = 20 % 7 //result === 6
```

A reminder by zero is always `NaN`, a special value that means "Not a Number":

```js
1 % 0 //NaN
-1 % 0 //NaN
```

## Multiplication (*)

Multiply two numbers

```js
1 * 2 //2
-1 * 2 //-2
```

## Exponentiation (**)

Raise the first operand to the power second operand

```js
1 ** 2 //1
2 ** 1 //2
2 ** 2 //4
2 ** 8 //256
8 ** 2 //64
```

The exponentiation operator `**` is the equivalent of using `Math.pow()`, but brought into the language instead of being a library function.

```js
Math.pow(4, 2) == 4 ** 2
```

This feature is a nice addition for math intensive JS applications.

The `**` operator is standardized across many languages including Python, Ruby, MATLAB, Lua, Perl and many others.

## Increment (++)

Increment a number. This is a unary operator, and if put before the number, it returns the value incremented.

If put after the number, it returns the original value, then increments it.

```js
let x = 0
x++ //0
x //1
++x //2
```

## Decrement (`--`)

Works like the increment operator, except it decrements the value.

```js
let x = 0
x-- //0
x //-1
--x //-2
```

## Unary negation (-)

Return the negation of the operand

```js
let x = 2
-x //-2
x //2
```

## Unary plus (+)

If the operand is not a number, it tries to convert it. Otherwise if the operand is already a number, it does nothing.

```js
let x = 2
+x //2

x = '2'
+x //2

x = '2a'
+x //NaN
```
