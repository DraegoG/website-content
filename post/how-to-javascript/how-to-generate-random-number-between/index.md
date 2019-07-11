---
title: How to generate a random number between two numbers in JavaScript
description: "The simplest possible way to randomly pick a number between two"
date: 2018-10-20T07:00:00+02:00
tags: js
---

Use a combination of `Math.floor()` and `Math.random()`.

This simple one line of code will return you a number between 1 and 6 (both included):

```js
Math.floor(Math.random() * 6 + 1)
```

There are 6 possible outcomes here: 1, 2, 3, 4, 5, 6.