---
title: The JavaScript `in` operator
date: 2019-06-29T07:00:00+02:00
description: "Learn the basics of the JavaScript `in` Operator"
tags: js
---

The `in` operator is pretty useful. It allows us to check if an object has a property.

This operator returns `true` if the first operand is a property of the object passed on the right, or a property of one of its ancestors in its prototype chain.

Otherwise it returns `false`.

Example:

```js
class Car {
  constructor() {
    this.wheels = 4
  }
}
class Fiesta extends Car {
  constructor() {
    super()
    this.brand = 'Ford'
  }
}

const myCar = new Fiesta()
'brand' in myCar //true
'wheels' in myCar //true
```
