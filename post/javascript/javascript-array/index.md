---
title: JavaScript Arrays, a definitive cheat sheet
description: "JavaScript arrays over time got more and more features, sometimes it's tricky to know when to use some construct vs another. This post aims to explain what you should use, as of 2019"
date: 2017-08-24T11:04:59+02:00
updated: 2019-01-17T11:04:59+02:00
booktitle: "Arrays"
tags: js
tags_weight: 15
---

<!-- TOC -->

- [Initialize array](#initialize-array)
- [Get length of the array](#get-length-of-the-array)
- [Iterating the array](#iterating-the-array)
  - [Every](#every)
  - [Some](#some)
  - [Iterate the array and return a new one with the returned result of a function](#iterate-the-array-and-return-a-new-one-with-the-returned-result-of-a-function)
  - [Filter an array](#filter-an-array)
  - [Reduce](#reduce)
  - [forEach](#foreach)
  - [for..of](#forof)
  - [for](#for)
  - [@@iterator](#iterator)
- [Adding to an array](#adding-to-an-array)
  - [Add at the end](#add-at-the-end)
  - [Add at the beginning](#add-at-the-beginning)
- [Removing an item from an array](#removing-an-item-from-an-array)
  - [From the end](#from-the-end)
  - [From the beginning](#from-the-beginning)
  - [At a random position](#at-a-random-position)
  - [Remove and insert in place](#remove-and-insert-in-place)
- [Join multiple arrays](#join-multiple-arrays)
- [Lookup the array for a specific element](#lookup-the-array-for-a-specific-element)
  - [ES5](#es5)
  - [ES2015](#es2015)
  - [ES2016](#es2016)
- [Get a portion of an array](#get-a-portion-of-an-array)
- [Sort the array](#sort-the-array)
- [Get a string representation of an array](#get-a-string-representation-of-an-array)
- [Copy an existing array by value](#copy-an-existing-array-by-value)
- [Copy just some values from an existing array](#copy-just-some-values-from-an-existing-array)
- [Copy portions of an array into the array itself, in other positions](#copy-portions-of-an-array-into-the-array-itself-in-other-positions)

<!-- /TOC -->

[JavaScript](/javascript/) arrays over time got more and more features, sometimes it's tricky to know when to use some construct vs another. This post aims to explain what you should use in 2018.

## Initialize array

```js
const a = []
const a = [1, 2, 3]
const a = Array.of(1, 2, 3)
const a = Array(6).fill(1) //init an array of 6 items of value 1
```

Don't use the old syntax (just use it for typed arrays)

```js
const a = new Array() //never use
const a = new Array(1, 2, 3) //never use
```

## Get length of the array

```js
const l = a.length
```

## Iterating the array

### Every

```js
a.every(f)
```

Iterates `a` until `f()` returns false

### Some

```js
a.some(f)
```

Iterates `a` until `f()` returns true

### Iterate the array and return a new one with the returned result of a function

Calling `map()` on an array will create a new array with the result of a function executed on every item of the original array:

```js
const a = [1, 2, 3]
const b = a.map((v, k) => v * k)
// b = [0, 2, 6]
```

This example:

```js
const b = a.map(f)
```

Iterates `a` and builds a new array with the result of executing `f()` on each `a` element

### Filter an array

```js
const b = a.filter(f)
```

Iterates `a` and builds a new array with elements of `a` that returned true when executing `f()` on each `a` element

### Reduce

```js
a.reduce((accumulator, currentValue, currentIndex, array) => {
  //...
}, initialValue)
```

`reduce()` executes a callback function on all the items of the array and allows to progressively compute a result. If `initialValue` is specified, `accumulator` in the first iteration will equal to that value.

Example:

```js
;[1, 2, 3, 4].reduce((accumulator, currentValue, currentIndex, array) => {
  return accumulator * currentValue
}, 1)

// iteration 1: 1 * 1 => return 1
// iteration 2: 1 * 2 => return 2
// iteration 3: 2 * 3 => return 6
// iteration 4: 6 * 4 => return 24

// return value is 24
```

### forEach

> ES6

```js
a.forEach(f)
```

Iterates `f` on `a` without a way to stop

Example:

```js
a.forEach(v => {
  console.log(v)
})
```

### for..of

> ES6

```js
for (let v of a) {
  console.log(v)
}
```

### for

```js
for (let i = 0; i < a.length; i += 1) {
  //a[i]
}
```

Iterates `a`, can be stopped using `return` or `break` and an iteration can be skipped using `continue`

### @@iterator

> ES6

Getting the iterator from an array returns an iterator of values

```js
const a = [1, 2, 3]
let it = a[Symbol.iterator]()

console.log(it.next().value) //1
console.log(it.next().value) //2
console.log(it.next().value) //3
```

`.entries()` returns an iterator of key/value pairs

```js
let it = a.entries()

console.log(it.next().value) //[0, 1]
console.log(it.next().value) //[1, 2]
console.log(it.next().value) //[2, 3]
```

`.keys()` allows to iterate on the keys:

```js
let it = a.keys()

console.log(it.next().value) //0
console.log(it.next().value) //1
console.log(it.next().value) //2
```

`.next()` returns `undefined` when the array ends. You can also detect if the iteration ended by looking at `it.next()` which returns a `value, done` pair. `done` is always false until the last element, which returns `true`.

## Adding to an array

### Add at the end

```js
a.push(4)
```

### Add at the beginning

```js
a.unshift(0)
a.unshift(-2, -1)
```

## Removing an item from an array

### From the end

```js
a.pop()
```

### From the beginning

```js
a.shift()
```

### At a random position

```js
a.splice(0, 2) // get the first 2 items
a.splice(3, 2) // get the  2 items starting from index 3
```

Do not use `remove()` as it leaves behind undefined values.

### Remove and insert in place

```js
a.splice(2, 3, 2, 'a', 'b') //removes 3 items starting from
//index 2, and adds 2 items,
// still starting from index 2
```

## Join multiple arrays

```js
const a = [1, 2]
const b = [3, 4]
a.concat(b) // 1, 2, 3, 4
```

## Lookup the array for a specific element

### ES5

```js
a.indexOf()
```

Returns the index of the first matching item found, or -1 if not found

```js
a.lastIndexOf()
```

Returns the index of the last matching item found, or -1 if not found

### ES2015

```js
a.find((element, index, array) => {
  //return true or false
})
```

Returns the first item that returns true. Returns undefined if not found.

A commonly used syntax is:

```js
a.find(x => x.id === my_id)
```

The above line will return the first element in the array that has `id === my_id`.

`findIndex` returns the index of the first item that returns true, and if not found, it returns `undefined`:

```js
a.findIndex((element, index, array) => {
  //return true or false
})
```

### ES2016

```js
a.includes(value)
```

Returns true if `a` contains `value`.

```js
a.includes(value, i)
```

Returns true if `a` contains `value` after the position `i`.

## Get a portion of an array

```js
a.slice()
```

## Sort the array

Sort alphabetically (by ASCII value - `0-9A-Za-z`)

```js
const a = [1, 2, 3, 10, 11]
a.sort() //1, 10, 11, 2, 3

const b = [1, 'a', 'Z', 3, 2, 11]
b = b.sort() //1, 11, 2, 3, Z, a
```

Sort by a custom function

```js
const a = [1, 10, 3, 2, 11]
a.sort((a, b) => a - b) //1, 2, 3, 10, 11
```

Reverse the order of an array

```js
a.reverse()
```

## Get a string representation of an array

```js
a.toString()
```

Returns a string representation of an array

```js
a.join()
```

Returns a string concatenation of the array elements.
Pass a parameter to add a custom separator:

```js
a.join(', ')
```

## Copy an existing array by value

```js
const b = Array.from(a)
const b = Array.of(...a)
```

## Copy just some values from an existing array

```js
const b = Array.from(a, x => x % 2 == 0)
```

## Copy portions of an array into the array itself, in other positions

```js
const a = [1, 2, 3, 4]
a.copyWithin(0, 2) // [3, 4, 3, 4]
const b = [1, 2, 3, 4, 5]
b.copyWithin(0, 2) // [3, 4, 5, 4, 5]
//0 is where to start copying into,
// 2 is where to start copying from
const c = [1, 2, 3, 4, 5]
c.copyWithin(0, 2, 4) // [3, 4, 3, 4, 5]
//4  is an end index
```
