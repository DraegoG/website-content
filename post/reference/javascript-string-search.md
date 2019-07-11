---
title: "The String search() method"
description: "Find out all about the JavaScript search() method of a string"
date: 2019-02-12T07:00:00+02:00
tags: js
---

Return the position of the first occurrence of the string `str` in the current string.

It returns the index of the start of the occurrence, or -1 if no occurrence is found.

```js
'JavaScript'.search('Script') //4
'JavaScript'.search('TypeScript') //-1
```

You can search using a regular expression (and in reality, even if you pass a string, that's internally and transparently used as a regular expression too).

```js
'JavaScript'.search(/Script/) //4
'JavaScript'.search(/script/i) //4
'JavaScript'.search(/a+v/) //1
```