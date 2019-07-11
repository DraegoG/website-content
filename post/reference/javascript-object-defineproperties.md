---
title: "The Object defineProperties() method"
description: "Find out all about the JavaScript defineProperties() method of the Object object"
date: 2019-03-30T07:00:00+02:00
tags: js
---

Creates or configures multiple object properties at once.
Returns the object.

Takes 2 arguments. The first is an object upon which we're going to create or configure the properties. The second is an object of properties.

Example:

```js
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
console.log(dog.breed) //'Siberian Husky'
```

I didn't just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.

It can be used in conjunction with [`Object.getOwnPropertyDescriptors()`](/javascript-object-getownpropertydescriptors/) to copy properties over from another object:

```js
const wolf = { /*... */ }
const dog = {}
Object.defineProperties(dog, Object.getOwnPropertyDescriptors(wolf))
```