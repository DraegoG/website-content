---
title: "The Object hasOwnProperty() method"
description: "Find out all about the JavaScript hasOwnProperty() method of an object"
date: 2019-04-17T07:00:00+02:00
tags: js
---

Called on an object instance, accepts a string as argument. If the object has a property with the name contained in the string argument, it returns `true`. Otherwise it returns `false`.

Example:

```js
const person = { name: 'Fred', age: 87 }
person.hasOwnProperty('name') //true
person.hasOwnProperty('job') //false
```