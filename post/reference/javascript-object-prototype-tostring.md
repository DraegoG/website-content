---
title: "The Object toString() method"
description: "Find out all about the JavaScript toString() method of an object"
date: 2019-04-21T07:00:00+02:00
tags: js
---

Called on an object instance, returns a string representation of the object.
Returns the `[object Object]` string unless overridden. Objects can then return a string representation of themselves.

```js
const person = { name: 'Fred' }
person.toString() //[object Object]
```