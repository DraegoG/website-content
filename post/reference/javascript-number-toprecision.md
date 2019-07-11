---
title: "The Number toPrecision() method"
description: "Find out all about the JavaScript toPrecision() method of a number"
date: 2019-03-21T07:00:00+02:00
tags: js
---

This method returns a string representing the number to a specified precision:

```js
new Number(21.2).toPrecision(0) //error! argument must be > 0
new Number(21.2).toPrecision(1) //2e+1 (= 2 * 10^1 = 2)
new Number(21.2).toPrecision(2) //21
new Number(21.2).toPrecision(3) //21.2
new Number(21.2).toPrecision(4) //21.20
new Number(21.2).toPrecision(5) //21.200
```