---
title: "The String startsWith() method"
description: "Find out all about the JavaScript startsWith() method of a string"
date: 2019-03-02T07:00:00+02:00
tags: js
---

Check if a string starts with the value of the string `str`

You can call `startsWith()` on any string, provide a substring, and check if the result returns `true` or `false`:

```js
'testing'.startsWith('test') //true
'going on testing'.startsWith('test') //false
```

This method accepts a second parameter, which lets you specify at which character you want to start checking:

```js
'testing'.startsWith('test', 2) //false
'going on testing'.startsWith('test', 9) //true
```