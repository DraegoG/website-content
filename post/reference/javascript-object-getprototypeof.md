---
title: "The Object getPrototypeOf() method"
description: "Find out all about the JavaScript getPrototypeOf() method of the Object object"
date: 2019-04-07T07:00:00+02:00
tags: js
---

Returns the prototype of an object.

Usage:

```js
Object.getPrototypeOf(obj)
```

Example:

```js
const animal = {}
const dog = Object.create(animal)
const prot = Object.getPrototypeOf(dog)

animal === prot //true
```

If the object has no prototype, we'll get `null`. This is the case of the Object object:

```js
Object.prototype //{}
Object.getPrototypeOf(Object.prototype) //null
```
