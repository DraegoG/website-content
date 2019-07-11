---
title: Dynamically select a method of an object in JavaScript
description: "Learn how to access a method of an object dynamically in JavaScript"
date: 2019-01-12T07:00:00+02:00
tags: js
---

Sometimes you have an object and you need to call a method, or a different method, depending on some condition.

For example you have a `car` object and you either want to `drive()` it or to `park()` it, depending on the `driver.sleepy` value.

If the driver has a sleepy level over 6, we need to park the car before it fells asleep while driving.

Here is how you achieve this with an `if/else` condition:

```js
if (driver.sleepy > 6) {
  car.park()
} else {
  car.drive()
}
```

Let's rewrite this to be more dynamic.

We can use the ternary operator to dynamically choose the method name, get it as the string value.

Using square brackets we can select it from the object's available methods:

```js
car[driver.sleepy > 6 ? 'park' : 'drive']
```

With the above statement we get the method reference. We can directly invoke it by appending the parentheses:

```js
car[driver.sleepy > 6 ? 'park' : 'drive']()
```