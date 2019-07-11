---
title: JavaScript Expressions
date: 2018-03-17T16:04:59+02:00
description: "Expressions are units of code that can be evaluated and resolve to a value. Expressions in JS can be divided in categories."
booktitle: Expressions
tags: js
tags_weight: 6
---

<!-- TOC -->

- [Arithmetic expressions](#arithmetic-expressions)
- [String expressions](#string-expressions)
- [Primary expressions](#primary-expressions)
- [Array and object initializers expressions](#array-and-object-initializers-expressions)
- [Logical expressions](#logical-expressions)
- [Left-hand-side expressions](#left-hand-side-expressions)
- [Property access expressions](#property-access-expressions)
- [Object creation expressions](#object-creation-expressions)
- [Function definition expressions](#function-definition-expressions)
- [Invocation expressions](#invocation-expressions)

<!-- /TOC -->

## Arithmetic expressions

Under this category go all expressions that evaluate to a number:

```js
1 / 2
i++
i -= 2
i * 2
```

## String expressions

Expressions that evaluate to a string:

```js
'A ' + 'string'
```

## Primary expressions

Under this category go variable references, literals and constants:

```js
2
0.02
'something'
true
false
this //the current object
undefined
i //where i is a variable or a constant
```

but also some language keywords:

```js
function
class
function* //the generator function
yield //the generator pauser/resumer
yield* //delegate to another generator or iterator
async function* //async function expression
await //async function pause/resume/wait for completion
/pattern/i //regex
() // grouping
```

## Array and object initializers expressions

```js
[] //array literal
{} //object literal
[1,2,3]
{a: 1, b: 2}
{a: {b: 1}}
```

## Logical expressions

Logical expressions make use of logical operators and resolve to a boolean value:

```js
a && b
a || b
!a
```

## Left-hand-side expressions

```js
new //create an instance of a constructor
super //calls the parent constructor
...obj //expression using the spread operator
```

> See the [**spread operator**](/javascript-spread-operator/) tutorial

## Property access expressions


```js
object.property //reference a property (or method) of an object
object[property]
object['property']
```

## Object creation expressions

```js
new object()
new a(1)
new MyRectangle('name', 2, {a: 4})
```

## Function definition expressions

```js
function() {}
function(a, b) { return a * b }
(a, b) => a * b
a => a * 2
() => { return 2 }
```

## Invocation expressions

The syntax for calling a function or method

```js
a.x(2)
window.resize()
```
