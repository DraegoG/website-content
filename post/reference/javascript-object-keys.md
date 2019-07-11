---
title: "The Object keys() method"
description: "Find out all about the JavaScript keys() method of the Object object"
date: 2019-04-12T07:00:00+02:00
tags: js
---

`Object.keys()` accepts an object as argument and returns an array of all its (own) enumerable properties.

```js
const car = {
  color: 'Blue',
  brand: 'Ford',
  model: 'Fiesta'
}

Object.keys(car) //[ 'color', 'brand', 'model' ]
```

I said enumerable properties. This means their internal enumerable flag is set to true, which is the default. [Check MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties) for more info on this subject.

One use of the `Object.keys` function is to create a copy of an object that has all the properties of it, except one:

```js
const car = {
  color: 'blue',
  brand: 'Ford'
}
const prop = 'color'

const newCar = Object.keys(car).reduce((object, key) => {
  if (key !== prop) {
    object[key] = car[key]
  }
  return object
}, {})
```
