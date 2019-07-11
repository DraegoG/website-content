---
title: JavaScript Types
date: 2018-02-14T16:04:59+02:00
updated: 2019-01-10T16:04:59+02:00
description: "You might sometimes read that JS is untyped, but that's incorrect. It's true that you can assign all sorts of different types to a variable, but JavaScript has types. In particular, it provides primitive types, and object types."
booktitle: Types
tags: js
tags_weight: 5
---

<!-- TOC -->

- [Primitive types](#primitive-types)
- [Numbers](#numbers)
- [Strings](#strings)
  - [Template literals](#template-literals)
- [Booleans](#booleans)
- [null](#null)
- [undefined](#undefined)
- [Object types](#object-types)
- [How to find the type of a variable](#how-to-find-the-type-of-a-variable)

<!-- /TOC -->

## Primitive types

Primitive types are

- [Number](/javascript-number/)
- [String](/javascript-string/)
- Boolean
- Symbol

And two special types:

- null
- undefined

Let's see them in detail in the next sections.

## Numbers

Internally, [JavaScript](/javascript/) has just one type for numbers: every number is a float.

A numeric literal is a number represented in the source code, amd depending on how it's written, it can be an integer literal or a floating point literal.

Integers:

```js
10
5354576767321
0xCC //hex
```

Floats:

```js
3.14
.1234
5.2e4 //5.2 * 10^4
```

## Strings

A string type is a sequence of characters. It's defined in the source code as a string literal, which is enclosed in quotes or double quotes

```js
'A string'
"Another string"
```

Strings can span across multiple lines by using the backslash

```js
"A \
string"
```

A string can contain escape sequences that can be interpreted when the string is printed, like \n to create a new line. The backslash is also useful when you need to enter for example a quote in a string enclosed in quotes, to prevent the char to be interpreted as a closing quote:

```js
'I\'m a developer'
```

Strings can be joined using the + operator:

```js
"A " + "string"
```

### Template literals

Introduced in ES2015, template literals are string literals that allow a more powerful way to define strings.

```js
const a_string = `something`
```

You can perform string substitution, embedding the result of any JS expression:

```js
`a string with ${something}`
`a string with ${something+somethingElse}`
`a string with ${obj.something()}`
```

You can have multiline strings easily:

```js
`a string
with
${something}`
```

## Booleans

JavaScript defines two reserved words for booleans: true and false.
Many comparision operations `==` `===` `<` `>` (and so on) return either one or the other.

`if`, `while` statements and other control structures use booleans to determine the flow of the program.

They don't just accept true or false, but also accept **truthy** and **falsy** values.

Falsy values, values **interpreted as false**, are

```js
0
-0
NaN
undefined
null
'' //empty string
```

All the rest is considered a **truthy value**.

## null

`null` is a special value that indicates the absence of a value.

It's a common concept in other languages as well, can be known as `nil` or `None` in Python for example.

## undefined

`undefined` indicates that a variable has not been initialized and the value is absent.

It's commonly returned by functions with no `return` value.
When a function accepts a parameter but that's not set by the caller, it's undefined.

To detect if a value is `undefined`, you use the construct:

```js
typeof variable === 'undefined'
```

## Object types

Anything that's not a primitive type is an [object](/javascript-object/) type.

Object types have properties and also have methods that can act on those properties.

## How to find the type of a variable

Any variable has a type assigned. Use the `typeof` operator to get a string representation of a type:

```js
typeof 1 === 'number'
typeof '1' === 'string'
typeof {name: 'Flavio'} === 'object'
typeof [1, 2, 3] === 'object'
typeof true === 'boolean'
typeof undefined === 'undefined'
typeof (() => {}) === 'function'
```

Why `typeof` returned "function"? JavaScript has no `function` type.
That's true, and that's a quirk of `typeof` which conveniently returns that value.