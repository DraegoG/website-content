---
title: "The Object isExtensible() method"
description: "Find out all about the JavaScript isExtensible() method of the Object object"
date: 2019-04-09T07:00:00+02:00
tags: js
---

This method checks if we can add new properties to an object.

Any object is extensible, unless it's been used as an argument to

- [`Object.freeze()`](/javascript-object-freeze/)
- [`Object.seal()`](/javascript-object-seal/)
- [`Object.preventExtensions()`](/javascript-object-preventextensions/)

Usage:

```js
const dog = {}
Object.isExtensible(dog) //true
```

```js
const cat = {}
Object.freeze(cat)
Object.isExtensible(cat) //false
```