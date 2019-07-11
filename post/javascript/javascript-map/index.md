---
title: "The JavaScript map() Function"
date: 2019-06-23T07:00:15+02:00
description: "The details of the `map()` Function in JavaScript"
tags: js
---

`map()` is key method of an array when it comes to thinking in functional programming terms.

This example iterates `a` and builds a new array with the result of executing `f()` on each `a` element:

```js
const b = a.map(f)
```

Given an array, we can use `map()` to create a new array from the initial one, and then filtering the result using `filter()`. This short example creates a new array to get the first letter of each item in the `list` array, and filters the one that matches `A`:

```js
const list = ['Apple', 'Orange', 'Egg']
list.map(item => item[0]).filter(item => item === 'A') //'A'
```