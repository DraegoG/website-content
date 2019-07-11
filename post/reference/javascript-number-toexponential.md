---
title: "The Number toExponential() method"
description: "Find out all about the JavaScript toExponential() method of a number"
date: 2019-03-22T07:00:00+02:00
tags: js
---

You can use this method to get a string representing the number in exponential notation:

```js
new Number(10).toExponential() //1e+1 (= 1 * 10^1)
new Number(21.2).toExponential() //2.12e+1 (= 2.12 * 10^1)
```

You can pass an argument to specify the fractional part digits:

```js
new Number(21.2).toExponential(1) //2.1e+1
new Number(21.2).toExponential(5) //2.12000e+1
```

Notice how we lost precision in the first example.