---
title: "The Number isInteger() method"
description: "Find out all about the JavaScript isInteger() method of the Number object"
date: 2019-03-14T07:00:00+02:00
tags: js
---

Returns true if the passed value is an integer. Anything else, booleans, strings, objects, arrays, returns false:

```js
Number.isInteger(1) //true
Number.isInteger(-237) //true
Number.isInteger(0) //true

Number.isInteger(0.2) //false
Number.isInteger('Flavio') //false
Number.isInteger(true) //false
Number.isInteger({}) //false
Number.isInteger([1, 2, 3]) //false
```
