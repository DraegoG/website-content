---
title: "The Object entries() method"
description: "Find out all about the JavaScript entries() method of the Object object"
date: 2019-04-01T07:00:00+02:00
tags: js
---

Introduced in `ES2017`.

This method returns an array containing all the object own properties, as an array of `[key, value]` pairs.

Usage:

```js
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
```

[`Object.entries()`](/javascript-object-entries/) also works with arrays:

```js
const people = ['Fred', 'Tony']
Object.entries(people) // [['0', 'Fred'], ['1', 'Tony']]
```

You can use it to count the number of properties an object contains, combined with the `length` property of the array.
