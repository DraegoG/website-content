---
title: "How to remove an item from an Array in JavaScript"
date: 2018-05-02T07:06:15+02:00
description: "JavaScript offers many ways to remove an item from an array. Learn the canonical way, and also find out all the options you have, using plain JavaScript"
tags: js
so: true
---

Here are a few ways to **remove an item from an array using JavaScript**.

All the method described **do not mutate the original array**, and instead create a new one.

## If you know the index of an item

Suppose you have an array, and you want to remove an item in position `i`.

One method is to use `slice()`:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const i = 2
const filteredItems = items.slice(0, i).concat(items.slice(i + 1, items.length))
// ["a", "b", "d", "e", "f"]
```

`slice()` creates a new array with the indexes it receives. We create a new array, from the start to the index we want to remove, and concatenate another array from the first position following the one we removed to the end of the array.

## If you know the value

In this case, one good option is to use `filter()`, which offers a more _declarative_ approach:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const valueToRemove = 'c'
const filteredItems = items.filter(item => item !== valueToRemove)
// ["a", "b", "d", "e", "f"]
```

This uses the ES6 arrow functions. You can use the traditional functions to support older browsers:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const valueToRemove = 'c'
const filteredItems = items.filter(function(item) {
  return item !== valueToRemove
})
// ["a", "b", "d", "e", "f"]
```

or you can use Babel and transpile the ES6 code back to ES5 to make it more digestible to old browsers, yet write modern JavaScript in your code.

## Removing multiple items

What if instead of a single item, you want to remove many items?

Let's find the simplest solution.

### By index

You can just create a function and remove items in series:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']

const removeItem = (items, i) =>
  items.slice(0, i-1).concat(items.slice(i, items.length))

let filteredItems = removeItem(items, 3)
filteredItems = removeItem(filteredItems, 5)
//["a", "b", "c", "d"]
```

### By value

You can search for inclusion inside the callback function:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const valuesToRemove = ['c', 'd']
const filteredItems = items.filter(item => !valuesToRemove.includes(item))
// ["a", "b", "e", "f"]
```

## Avoid mutating the original array

`splice()` (not to be confused with `slice()`) mutates the original array, and should be avoided.