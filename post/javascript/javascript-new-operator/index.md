---
title: JavaScript new Operator
date: 2019-05-05T07:00:00+02:00
description: "Learn the basics of the JavaScript new Operator"
tags: js
---

The JavaScript `new` operator is used to create a new object.

You follow `new` with the object class to create a new object of that type:

```js
const date = new Date()
```

If the object constructor accepts parameters, we pass them:

```js
const date = new Date('2019-04-22')
```

Given an Object constructor like this:

```js
function Car(brand, model) {
  this.brand = brand
  this.model = model
}
```

We initialize a new "Car" object using:

```js
const myCar = new Car('Ford', 'Fiesta')
myCar.brand //'Ford'
myCar.model //'Fiesta'
```
