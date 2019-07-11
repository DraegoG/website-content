---
title: JavaScript instanceof Operator
date: 2019-05-18T07:00:00+02:00
description: "Learn the basics of the JavaScript instanceof Operator"
tags: js
---

The JavaScript `instanceof ` operator returns true if the first operand is an instance of the object passed on the right, or one of its ancestors in its prototype chain.

In this example you can see that the `myCar` object, of class Fiesta, responds true to `instanceof Fiesta`, and also responds true to `instanceOf Car`, because Fiesta extends Car:

```js
class Car {}
class Fiesta extends Car {}

const myCar = new Fiesta()
myCar instanceof Fiesta //true
myCar instanceof Car //true
```
