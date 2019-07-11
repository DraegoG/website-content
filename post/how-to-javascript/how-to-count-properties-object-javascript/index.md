---
title: How to count the number of properties in a JavaScript object
date: 2018-12-07T07:00:00+02:00
description: "Find out how to calculate how many properties has a JavaScript object"
tags: js
---

Use the [`Object.keys()`](/javascript-object-keys/) method, passing the object you want to inspect, to get an array of all the (own) enumerable properties of the object.

Then calculate the length of that array by checking the `length` property:

```js
const car = {
  color: 'Blue',
  brand: 'Ford',
  model: 'Fiesta'
}

Object.keys(car).length
```

I said enumerable properties. This means their internal enumerable flag is set to true, which is the default. [Check MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties) for more info on this subject.