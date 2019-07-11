---
title: "The JavaScript Math object"
description: "The Math object contains lots of utilities math-related. This tutorial describes them all"
date: 2018-07-18T07:06:29+02:00
booktitle: "The Math Object"
tags: js
tags_weight: 32

---

The Math object contains lots of utilities math-related.

It contains constants and functions.

## Constants

Item | Description
---------|----------
`Math.E` | The constant _e_, base of the natural logarithm (means ~2.71828)
`Math.LN10` | The constant that represents the base _e_ (natural) logarithm of 10
`Math.LN2` | The constant that represents the base _e_ (natural) logarithm of 2
`Math.LOG10E` | The constant that represents the base 10 logarithm of _e_
`Math.LOG2E` | The constant that represents the base 2 logarithm of _e_
`Math.PI` | The π constant (~3.14159)
`Math.SQRT1_2` | The constant that represents the reciprocal of the square root of 2
`Math.SQRT2` | The constant that represents the square root of 2

## Functions

All those functions are static. Math cannot be instantiated.

### Math.abs()

Returns the absolute value of a number

```js
Math.abs(2.5) //2.5
Math.abs(-2.5) //2.5
```

### Math.acos()

Returns the arccosine of the operand

The operand must be between -1 and 1

```js
Math.acos(0.8) //0.6435011087932843
```

### Math.asin()

Returns the arcsine of the operand

The operand must be between -1 and 1

```js
Math.asin(0.8) //0.9272952180016123
```

### Math.atan()

Returns the arctangent of the operand

```js
Math.atan(30) //1.5374753309166493
```

### Math.atan2()

Returns the arctangent of the quotient of its arguments.

```js
Math.atan2(30, 20) //0.982793723247329
```

### Math.ceil()

Rounds a number up

```js
Math.ceil(2.5) //3
Math.ceil(2) //2
Math.ceil(2.1) //3
Math.ceil(2.99999) //3
```

### Math.cos()

Return the cosine of an angle expressed in radiants

```js
Math.cos(0) //1
Math.cos(Math.PI) //-1
```

### Math.exp()

Return the value of Math.E multiplied per the exponent that's passed as argument

```js
Math.exp(1) //2.718281828459045
Math.exp(2) //7.38905609893065
Math.exp(5) //148.4131591025766
```

### Math.floor()

Rounds a number down

```js
Math.floor(2.5) //2
Math.floor(2) //2
Math.floor(2.1) //2
Math.floor(2.99999) //2
```

### Math.log()

Return the base _e_ (natural) logarithm of a number

```js
Math.log(10) //2.302585092994046
Math.log(Math.E) //1
```

### Math.max()

Return the highest number in the set of numbers passed

```js
Math.max(1,2,3,4,5) //5
Math.max(1) //1
```

### Math.min()

Return the smallest number in the set of numbers passed

```js
Math.max(1,2,3,4,5) //1
Math.max(1) //1
```

### Math.pow()

Return the first argument raised to the second argument

```js
Math.pow(1, 2) //1
Math.pow(2, 1) //2
Math.pow(2, 2) //4
Math.pow(2, 4) //16
```

### Math.random()

Returns a pseudorandom number between 0.0 and 1.0

```js
Math.random() //0.9318168241227056
Math.random() //0.35268950194094395
```

### Math.round()

Rounds a number to the nearest integer

```js
Math.round(1.2) //1
Math.round(1.6) //2
```

### Math.sin()

Calculates the sin of an angle expressed in radiants

```js
Math.sin(0) //0
Math.sin(Math.PI) //1.2246467991473532e-16)
```

### Math.sqrt()

Return the square root of the argument

```js
Math.sqrt(4) //2
Math.sqrt(16) //4
Math.sqrt(5) //2.23606797749979
```

### Math.tan()

Calculates the tangent of an angle expressed in radiants

```js
Math.tan(0) //0
Math.tan(Math.PI) //-1.2246467991473532e-16
```
