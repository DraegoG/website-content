---
title: this in JavaScript
date: 2018-05-16T07:04:59+02:00
description: "`this` is a value that has different values depending on where it's used. Not knowing this tiny detail of JavaScript can cause a lot of headaches, so it's worth taking 5 minutes to learn all the tricks"
tags: js
tags_weight: 26
---

`this` is a keyword that has different values depending on where it's used.

Not knowing this tiny detail of JavaScript can cause a lot of headaches, so it's worth taking 5 minutes to learn all the tricks.

## `this` in strict mode

Outside any object, `this` in **strict mode** is always `undefined`.

Notice I mentioned strict mode. If strict mode is disabled (the default state if you don't explicitly add `'use strict'` on top of your file ), you are in the so-called _sloppy mode_, and `this` - unless some specific cases mentioned here below - has the value of the global object.

Which means `window` in a browser context.

## `this` in methods

A method is a function attached to an object.

You can see it in various forms.

Here's one:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

car.drive()
//Driving a Ford Fiesta car!
```

In this case, using a regular function, `this` is automatically bound to the object.

Note: the above method declaration is the same as `drive: function() {`..., but shorter:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive: function() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}
```

The same works in this example:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

car.drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}

car.drive()
//Driving a Ford Fiesta car!
```

An arrow function does not work in the same way, as it's lexically bound:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive: () => {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

car.drive()
//Driving a undefined undefined car!
```

## Binding arrow functions

You cannot bind a value to an arrow function, like you do with normal functions.

It's not possible due to the way they work. `this` is **lexically bound**, which means its value is derived from the context where they are defined.

## Explicitly pass an object to be used as `this`

JavaScript offers a few ways to map `this` to any object you want.

Using `bind()`, at the **function declaration** step:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

const drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}.bind(car)

drive()
//Driving a Ford Fiesta car!
```

You could also bind an existing object method to remap its `this` value:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

const anotherCar = {
  maker: 'Audi',
  model: 'A4'
}

car.drive.bind(anotherCar)()
//Driving a Audi A4 car!
```

Using `call()` or `apply()`, at the **function invocation** step:

```js
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

const drive = function(kmh) {
  console.log(`Driving a ${this.maker} ${this.model} car at ${kmh} km/h!`)
}

drive.call(car, 100)
//Driving a Ford Fiesta car at 100 km/h!

drive.apply(car, [100])
//Driving a Ford Fiesta car at 100 km/h!
```

The first parameter you pass to `call()` or `apply()` is always bound to `this`.
The difference between call() and apply() is just that the second one wants an array as the arguments list, while the first accepts a variable number of parameters, which passes as function arguments.

## The special case of browser event handlers

In event handlers callbacks, `this` refers to the HTML element that received the event:

```js
document.querySelector('#button').addEventListener('click', function(e) {
  console.log(this) //HTMLElement
}
```

You can bind it using

```js
document.querySelector('#button').addEventListener(
  'click',
  function(e) {
    console.log(this) //Window if global, or your context
  }.bind(this)
)
```
