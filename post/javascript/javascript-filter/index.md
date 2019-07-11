---
title: "The JavaScript filter() Function"
date: 2019-06-22T07:06:15+02:00
description: "The details of the `filter()` Function in JavaScript"
tags: js
---

`filter()` is a very important method of an array.

This example iterates the array `a` and builds a new array with elements of `a` that returned true when running the function `f()` on each `a` element

```js
const b = a.filter(f)
```

A good example of using filter() is when you want to remove an item from the array:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const valueToRemove = 'c'
const filteredItems = items.filter(item => item !== valueToRemove)
// ["a", "b", "d", "e", "f"]
```

Here is how you could remove multiple items at the same time:

```js
const items = ['a', 'b', 'c', 'd', 'e', 'f']
const valuesToRemove = ['c', 'd']
const filteredItems = items.filter(item => !valuesToRemove.includes(item))
// ["a", "b", "e", "f"]
```
