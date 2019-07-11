---
title: JavaScript Logical Operators
date: 2019-06-10T07:00:00+02:00
description: "Learn the basics of the JavaScript Logical Operators"
tags: js
---

JavaScript provides us 3 logical operators: **and**, **or** and **not**.

## Logical and

Returns true if both operands are true:

```js
<expression> && <expression>
```

For example:

```js
a === true && b > 3
```

The cool thing about this operator is that the second expression is never executed if the first evaluates to false. Which has some practical applications, for example, to check if an object is defined before using it:

```js
const car = { color: 'green' }
const color = car && car.color
```

## Logical or

Returns true if at least one of the operands is true:

```js
<expression> || <expression>
```

For example:

```js
a === true || b > 3
```

This operator is very useful to fallback to a default value. For example:

```js
const car = {}
const color = car.color || 'green'
```

makes `color` default to `green` if `car.color` is not defined.

## Logical not (!)

Invert the value of a boolean:

```js
let value = true
!value //false
```
