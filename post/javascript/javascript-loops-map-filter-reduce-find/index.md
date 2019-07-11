---
title: Write JavaScript loops using map, filter, reduce and find
seotitle: Write JavaScript loops using map, filter, reduce and find
date: 2018-04-13T07:07:09+02:00
updated: 2018-04-16T07:07:09+02:00
description: "How to perform common operations in JavaScript where you might use loops, using map(), filter(), reduce() and find()"
booktitle: "An alternative approach to loops using map, filter, reduce and find"
tags: js
tags_weight: 43
---

[Loops](/javascript-loops/) are generally used, in any programming language, to perform operations on arrays: given an array you can iterate over its elements and perform a calculation.

Let's see how to pick common needs and perform them using a **[Functional Programming](/javascript-functional-programming/) approach**, as opposed to using loops.

> NOTE: I don't recommend one approach over the other. I just want to introduce different ways to perform the same thing and maybe introduce you to new functions which you might have never used until now.

## `map`, `filter`, `reduce`, `find`

Those are 3 really powerful array functions:

- `map` returns an array with the same length,
- `filter` as the name implies, it returns an array with less items than the original array
- `reduce` returns a single value (or object)
- `find` returns the first items in an array that satisfies a condition

`map`, `filter` and `reduce` were introduced in ES5, so you can safely use them as implemented in every browser since years.

`find` was introduced in ES6/ES2015.

They offer a more **declarative approach**, rather than an imperative approach (describe **what** should happen, not write every tiny bit of processing that should happen)

## Execute something on every element with `map`

A loop would look like this:

```js
const performSomething = (item) => {
  //...
  return item
}
const items = ['a', 'b', 'c']
items.forEach((item) => {
  performSomething(item)
})
```

With a declarative approach, you tell JavaScript to perform something on every element using:

```js
const items = ['a', 'b', 'c']
const newArray = items.map((item) => performSomething(item))
```

This generates a new array, without editing the original one (what we call immutability)

Since we use a single function in the map callback function, we can rewrite the sample as:

```js
const items = ['a', 'b', 'c']
const newArray = items.map(performSomething)
```

## Finding a single element in the array

Sometimes you need to look for a specific item in the array, and return it.

This is how you would do so with a loop:

```js
const items = [
  { name: 'a', content: { /* ... */ }},
  { name: 'b', content: { /* ... */ }},
  { name: 'c', content: { /* ... */ }}
]
for (const item of items) {
  if (item.name === 'b') {
    return item
  }
}
```

Here is the non-loop version, using `find()` (ES6+):

```js
const b = items.find((item) => item.name === 'b')
```

Here is the same functionality using `filter()` (ES5+):

```js
const b = items.filter((item) => item.name === 'b').shift()
```

> shift() returns the first item in the array without raising an error if the array is empty (returns `undefined` in that case).

Note: `shift()` mutates the array, but the array it mutates is the one returned by `filter()`, not the original array. If this sounds unacceptable, you can check if the array is not empty and get the first item using `b[0]`.

For learning purposes (does not make much sense in practice), here is the same functionality using [`reduce()`](/javascript-functional-programming/#arrayreduce):

```js
const items = [
  { name: 'a', content: { /* ... */ }},
  { name: 'b', content: { /* ... */ }},
  { name: 'c', content: { /* ... */ }}
]

const b = items.reduce((result, item) => {
  if (item.name === 'b') { result = item }
  return result
}, null)
```

`filter()` and `reduce()` will iterate over all the array items, while `find()` will be faster.

## Iterate over an array to count a property of each item

Use `reduce()` to get a single value out of an array. For example sum the items `content.value` property:

```js
const items = [
  { name: 'a', content: { value: 1 }},
  { name: 'b', content: { value: 2 }},
  { name: 'c', content: { value: 3 }}
]
```

using a loop:

```js
let count = 0
for (const item of items) {
  count += item.content.value
}
```

can written as

```js
const count = items.reduce((result, { content: { value } }) => result + value, 0)
```