---
title: "The Number isFinite() method"
description: "Find out all about the JavaScript isFinite() method of the Number object"
date: 2019-03-25T07:00:00+02:00
tags: js
---

Returns true if the passed value is a finite number. Anything else, booleans, strings, objects, arrays, returns false:

```js
Number.isFinite(1) //true
Number.isFinite(-237) //true
Number.isFinite(0) //true
Number.isFinite(0.2) //true

Number.isFinite('Flavio') //false
Number.isFinite(true) //false
Number.isFinite({}) //false
Number.isFinite([1, 2, 3]) //false
```