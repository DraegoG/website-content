---
title: How to check if a string starts with another in JavaScript
description: "Checking if a string starts with another substring is a common thing to do. See how to perform this check in JavaScript"
date: 2018-09-29T07:00:00+02:00
tags: js
---

ES6, introduced in 2015, added the `startsWith()` method to the String object prototype.

This is _the_ way to perform this check in 2018.

This means you can call `startsWith()` on any string, provide a substring, and check if the result returns `true` or `false`:

```js
'testing'.startsWith('test') //true
'going on testing'.startsWith('test') //false
```

This method accepts a second parameter, which lets you specify at which character you want to start checking:

```js
'testing'.startsWith('test', 2) //false
'going on testing'.startsWith('test', 9) //true
```