---
title: "The String indexOf() method"
description: "Find out all about the JavaScript indexOf() method of a string"
date: 2019-02-20T07:00:00+02:00
tags: js
---

Gives the position of the first occurrence of the string `str` in the current string. Returns -1 if the string is not found.

```js
'JavaScript'.indexOf('Script') //4
'JavaScript'.indexOf('JavaScript') //0
'JavaScript'.indexOf('aSc') //3
'JavaScript'.indexOf('C++') //-1
```

You can pass a second parameters to set the starting point:

```js
'a nice string'.indexOf('nice') !== -1 //true
'a nice string'.indexOf('nice', 3) !== -1 //false
'a nice string'.indexOf('nice', 2) !== -1 //true
```