---
title: "The Object isFrozen() method"
description: "Find out all about the JavaScript isFrozen() method of the Object object"
date: 2019-04-10T07:00:00+02:00
tags: js
---

Accepts an object as argument, and returns `true` if the object is frozen, `false` otherwise. Objects are frozen when they are return values of the [`Object.freeze()`](/javascript-object-freeze/) function.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.freeze(dog)
Object.isFrozen(dog) //true
Object.isFrozen(myDog) //true
dog === myDog //true
```

In the example, both `dog` and `myDog` are frozen. The argument passed as argument to `Object.freeze()` is mutated, and can't be un-freezed. It's also returned as argument, hence `dog` === `myDog` (it's the same exact object).
