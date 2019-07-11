---
title: "The Object freeze() method"
description: "Find out all about the JavaScript freeze() method of the Object object"
date: 2019-04-02T07:00:00+02:00
tags: js
---

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it's now an immutable object. No properties can be added, no properties can be removed, properties can't be changed.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
const myDog = Object.freeze(dog)

Object.isFrozen(dog) //true
Object.isFrozen(myDog) //true
dog === myDog //true

dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

> Also see [`Object.isFrozen()`](/javascript-object-isfrozen/)

In the example, both `dog` and `myDog` are frozen. The argument passed as argument to [`Object.freeze()`](/javascript-object-freeze/) is mutated, and can't be un-freezed. It's also returned as argument, hence `dog` === `myDog` (it's the same exact object).

Calling `Object.freeze()` is the equivalent of calling [`Object.preventExtensions()`](/javascript-object-preventextensions/) to prevent an object to have more properties defined, plus setting all properties as non-configurable and non-writeable.
