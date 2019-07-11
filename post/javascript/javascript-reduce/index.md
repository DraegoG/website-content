---
title: "The JavaScript reduce() Function"
date: 2019-06-24T07:00:15+02:00
description: "The details of the `reduce()` Function in JavaScript"
tags: js
---

`reduce()` is another important method of an array.

`reduce()` executes a callback function on all the items of the array and allows to progressively compute a result. If `initialValue` is specified, `accumulator` in the first iteration will equal to that value.

```js
a.reduce((accumulator, currentValue, currentIndex, array) => {
  //...
}, initialValue)
```

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
