---
title: "The Number toFixed() method"
description: "Find out all about the JavaScript toFixed() method of a number"
date: 2019-03-24T07:00:00+02:00
tags: js
---

You can use this method to get a string representing the number in fixed point notation:

```js
new Number(21.2).toFixed() //21
```

You can add an optional number setting the digits as a parameter:

```js
new Number(21.2).toFixed(0) //21
new Number(21.2).toFixed(1) //21.2
new Number(21.2).toFixed(2) //21.20
```