---
title: "The Object isSealed() method"
description: "Find out all about the JavaScript isSealed() method of the Object object"
date: 2019-04-11T07:00:00+02:00
tags: js
---

Accepts an object as argument, and returns `true` if the object is sealed, `false` otherwise. Objects are sealed when they are return values of the [`Object.seal()`](/javascript-object-seal/) function.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.seal(dog)
Object.isSealed(dog) //true
Object.isSealed(myDog) //true
dog === myDog //true
```

In the example, both `dog` and `myDog` are sealed. The argument passed as argument to [`Object.seal()`](/javascript-object-seal/) is mutated, and can't be un-sealed. It's also returned as argument, hence `dog` === `myDog` (it's the same exact object).
