---
title: "JavaScript Loops"
description: "JavaScript provides many way to iterate through loops. This tutorial explains all the various loop possibilities in modern JavaScript"
date: 2018-04-11T07:06:29+02:00
booktitle: "Loops"
tags: js
tags_weight: 16
---

<!-- TOC -->

- [Introduction](#introduction)
- [`for`](#for)
- [forEach](#foreach)
- [`do...while`](#dowhile)
- [`while`](#while)
- [`for...in`](#forin)
- [`for...of`](#forof)
- [`for...in` vs `for...of`](#forin-vs-forof)

<!-- /TOC -->

## Introduction

JavaScript provides many way to iterate through loops. This tutorial explains each one with a small example and the main properties.

## `for`

```js
const list = ['a', 'b', 'c']
for (let i = 0; i < list.length; i++) {
  console.log(list[i]) //value
  console.log(i) //index
}
```

- You can interrupt a `for` loop using `break`
- You can fast forward to the next iteration of a `for` loop using `continue`

## forEach

Introduced in ES5. Given an array, you can iterate over its properties using `list.forEach()`:

```js
const list = ['a', 'b', 'c']
list.forEach((item, index) => {
  console.log(item) //value
  console.log(index) //index
})

//index is optional
list.forEach(item => console.log(item))
```

unfortunately you cannot break out of this loop.

## `do...while`

```js
const list = ['a', 'b', 'c']
let i = 0
do {
  console.log(list[i]) //value
  console.log(i) //index
  i = i + 1
} while (i < list.length)
```

You can interrupt a `while` loop using `break`:

```js
do {
  if (something) break
} while (true)
```

and you can jump to the next iteration using `continue`:

```js
do {
  if (something) continue

  //do something else
} while (true)
```

## `while`

```js
const list = ['a', 'b', 'c']
let i = 0
while (i < list.length) {
  console.log(list[i]) //value
  console.log(i) //index
  i = i + 1
}
```

You can interrupt a `while` loop using `break`:

```js
while (true) {
  if (something) break
}
```

and you can jump to the next iteration using `continue`:

```js
while (true) {
  if (something) continue

  //do something else
}
```

The difference with `do...while` is that `do...while` always execute its cycle at least once.

## `for...in`

Iterates all the enumerable properties of an object, giving the property names.

```js
for (let property in object) {
  console.log(property) //property name
  console.log(object[property]) //property value
}
```

## `for...of`

[ES6](/es6/) introduced the `for...of` loop, which combines the conciseness of forEach with the ability to break:

```js
//iterate over the value
for (const value of ['a', 'b', 'c']) {
  console.log(value) //value
}

//get the index as well, using `entries()`
for (const [index, value] of ['a', 'b', 'c'].entries()) {
  console.log(index) //index
  console.log(value) //value
}
```

Notice the use of `const`. This loop creates a new scope in every iteration, so we can safely use that instead of `let`.

## `for...in` vs `for...of`

The difference with `for...in` is:

- `for...of` **iterates over the property values**
- `for...in` **iterates the property names**
