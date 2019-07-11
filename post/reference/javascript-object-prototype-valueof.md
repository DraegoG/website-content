---
title: "The Object valueOf() method"
description: "Find out all about the JavaScript valueOf() method of an object"
date: 2019-04-22T07:00:00+02:00
tags: js
---

Called on an object instance, returns the primitive value of it.

```js
const person = { name: 'Fred' }
person.valueOf() //{ name: 'Fred' }
```

This is normally only used internally by JavaScript, and rarely actually invoked in user code.