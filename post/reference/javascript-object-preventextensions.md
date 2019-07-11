---
title: "The Object preventExtensions() method"
description: "Find out all about the JavaScript preventExtensions() method of the Object object"
date: 2019-04-13T07:00:00+02:00
tags: js
---

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it's now an object that will not accept new properties. New properties *can't* be added, but existing properties *can* be removed, and existing properties *can* be changed.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
Object.preventExtensions(dog)

dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

The argument passed as argument is also returned as argument, hence `dog` === `myDog` (it's the same exact object).

We can't add new properties, but we can remove existing properties:

```js
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'
Object.preventExtensions(dog)
delete dog.name
dog //{ breed: 'Siberian Husky' }
```