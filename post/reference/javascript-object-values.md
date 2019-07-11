---
title: "The Object values() method"
description: "Find out all about the JavaScript values() method of the Object object"
date: 2019-04-16T07:00:00+02:00
tags: js
---

This method returns an array containing all the object own property values.

Usage:

```js
const person = { name: 'Fred', age: 87 }
Object.values(person) // ['Fred', 87]
```

`Object.values()` also works with arrays:

```js
const people = ['Fred', 'Tony']
Object.values(people) // ['Fred', 'Tony']
```