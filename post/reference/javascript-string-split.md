---
title: "The String split() method"
description: "Find out all about the JavaScript split() method of a string"
date: 2019-03-01T07:00:00+02:00
tags: js
---

`split()` truncates a string when it finds a pattern (case sensitive), and returns an array with the tokens:

```js
const phrase = 'I love my dog! Dogs are great'
const tokens = phrase.split('dog')

tokens //["I love my ", "! Dogs are great"]
```