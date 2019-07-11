---
title: "The Object toLocaleString() method"
description: "Find out all about the JavaScript toLocaleString() method of an object"
date: 2019-04-20T07:00:00+02:00
tags: js
---

Called on an object instance, returns a string representation of the object. Accepts an optional locale as argument.

Returns the `[object Object]` string unless overridden. Objects can then return a different string representation depending on the locale.

```js
const person = { name: 'Fred' }
person.toLocaleString() //[object Object]
```
