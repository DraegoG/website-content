---
title: "The Object seal() method"
description: "Find out all about the JavaScript seal() method of the Object object"
date: 2019-04-14T07:00:00+02:00
tags: js
---

Takes an object as argument, and returns the same object. The object passed as argument is mutated and it's now an object that will not accept new properties. New properties *can't* be added, and existing properties *can't* be removed, but existing properties *can* be changed.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
Object.seal(dog)
dog.breed = 'Pug'
dog.name = 'Roger' //TypeError: Cannot add property name, object is not extensible
```

The argument passed as argument is also returned as argument, hence `dog` === `myDog` (it's the same exact object).

Similar to [`Object.freeze()`](/javascript-object-freeze/) but does not make properties non-writable. In only prevents to add or remove properties.

Similar to [`Object.preventExtensions()`](/javascript-object-preventextensions/) but also disallows removing properties:

```js
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'
Object.seal(dog)
delete dog.name //TypeError: Cannot delete property 'name' of #<Object>
```