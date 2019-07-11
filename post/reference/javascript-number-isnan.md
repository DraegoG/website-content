---
title: "The Number isNaN() method"
description: "Find out all about the JavaScript isNaN() method of the Number object"
date: 2019-03-15T07:00:00+02:00
tags: js
---

`NaN` is a special case. A number is `NaN` only if it's `NaN` or if it's a division of 0 by 0 expression, which returns `NaN`. In all the other cases, we can pass it what we want but it will return `false`:

```js
Number.isNaN(NaN) //true
Number.isNaN(0 / 0) //true

Number.isNaN(1) //false
Number.isNaN('Flavio') //false
Number.isNaN(true) //false
Number.isNaN({}) //false
Number.isNaN([1, 2, 3]) //false
```
