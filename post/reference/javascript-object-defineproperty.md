---
title: "The Object defineProperty() method"
description: "Find out all about the JavaScript defineProperty() method of the Object object"
date: 2019-03-31T07:00:00+02:00
tags: js
---

Creates or configures one object property.

Returns the object.

Takes 3 arguments. The first is an object upon which we're going to create or configure the properties. The second is the property name defined as a string. The third is an object with the property definition.

Example:

```js
const dog = {}
Object.defineProperty(dog, 'breed', {
  value: 'Siberian Husky'
})
console.log(dog.breed) //'Siberian Husky'
```

I didn't just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.
