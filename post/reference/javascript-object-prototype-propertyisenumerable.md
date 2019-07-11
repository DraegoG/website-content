---
title: "The Object propertyIsEnumerable() method"
description: "Find out all about the JavaScript propertyIsEnumerable() method of an object"
date: 2019-04-19T07:00:00+02:00
tags: js
---

Called on an object instance, accepts a string as argument. If the object has a property with the name contained in the string argument, and that property is enumerable, it returns `true`. Otherwise it returns `false`.

Example:

```js
const person = { name: 'Fred' }

Object.defineProperty(person, 'age', {
  value: 87,
  enumerable: false
})

person.propertyIsEnumerable('name') //true
person.propertyIsEnumerable('age') //false
```