---
title: "JavaScript Reference: Object"
description: "All about the JavaScript Object properties and methods"
date: 2019-04-23T07:00:00+02:00
tags: js
---

This post documents all the `Object` built-in object properties and methods.

Any value that's not of a primitive type (a string, a number, a boolean, a symbol, null or undefined) is an **object**. Even arrays or functions are, under the hoods, objects.

An `object` value can be generated using an object literal syntax:

```js
const person = {}
typeof person //object
```

using the `Object` global function:

```js
const person = Object()
typeof person //object
```

or using the Object constructor:

```js
const person = new Object()
typeof person //object
```

Another syntax is to use `Object.create()`:

```js
const car = Object.create()
```

You can initialize the object with properties using this syntax:

```js
const person = {
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
}

const person = Object({
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
})

const person = new Object({
  age: 36,
  name: 'Flavio',
  speak: () => {
    //speak
  }
})
```

All those ways are basically equivalent as they all give you access to the methods I'll list below.

You can also initialize an object using the `new` keyword before a function with a capital letter. This function serves as a constructor for that object. In there, we can initialize the arguments we receive as parameters, to setup the initial state of the object:

```js
function Car(brand, model) {
  this.brand = brand
  this.model = model
}
```

We initialize a new object using

```js
const myCar = new Car('Ford', 'Fiesta')
myCar.brand //'Ford'
myCar.model //'Fiesta'
```

Objects have **properties**. Every property has a name and a value.

You might think an object is basically a _map_, or _dictionary_, data structure, and you would be correct.

The value of a property can be of any type, which means that it can even be an object, as objects can nest other objects.

When a property value is a function, we call it **method**.

Objects can inherit their properties from other objects, and we'll see this in details when we'll talk about inheritance.

Objects are **always passed by reference**.

If you assign a variable the same value of another, if it's a primitive type like a number or a string, they are passed by value:

```js
let age = 36
let myAge = age
myAge = 37
age //36
```

```js
const car = {
  color: 'blue'
}
const anotherCar = car
anotherCar.color = 'yellow'
car.color //'yellow'
```

## Built-in Object Properties

The Object object has 2 properties

- `length` always equal to `1`
- `prototype` this points to the Object prototype object: the object that all other objects inherit from. Check the [prototypal inheritance](/javascript-prototypal-inheritance/) post for more.

## Static methods

We divide methods in static methods, and instance methods. Static methods are called directly on `Object`. Instance methods are called on an object instance (`an` object).

Static methods are a great way to offer a namespace for functions that work in the same space. In this way we don't have global functions around, but all are namespaced under the `Object` global object.

- [`Object.assign()`](/javascript-object-assign/) *`ES2015`
- [`Object.create()`](/javascript-object-create/)
- [`Object.defineProperties()`](/javascript-object-defineproperties/)
- [`Object.defineProperty()`](/javascript-object-defineproperty/)
- [`Object.entries()`](/javascript-object-entries/) *`ES2017`
- [`Object.freeze()`](/javascript-object-freeze/)
- [`Object.getOwnPropertyDescriptor()`](/javascript-object-getownpropertydescriptor/)
- [`Object.getOwnPropertyDescriptors()`](/javascript-object-getownpropertydescriptors/)
- [`Object.getOwnPropertyNames()`](/javascript-object-getownpropertynames/)
- [`Object.getOwnPropertySymbols()`](/javascript-object-getownpropertysymbols/)
- [`Object.getPrototypeOf()`](/javascript-object-getprototypeof/)
- [`Object.is()`](/javascript-object-is/) *`ES2015`
- [`Object.isExtensible()`](/javascript-object-isextensible/)
- [`Object.isFrozen()`](/javascript-object-isfrozen/)
- [`Object.isSealed()`](/javascript-object-issealed/)
- [`Object.keys()`](/javascript-object-keys/)
- [`Object.preventExtensions()`](/javascript-object-preventextensions/)
- [`Object.seal()`](/javascript-object-seal/)
- [`Object.setPrototypeOf()`](/javascript-object-setprototypeof/) *`ES2015`
- [`Object.values()`](/javascript-object-values/)

## Instance methods

- [`hasOwnProperty()`](/javascript-object-prototype-hasownproperty/)
- [`isPrototypeOf()`](/javascript-object-prototype-isprototypeof/)
- [`propertyIsEnumerable()`](/javascript-object-prototype-propertyisenumerable/)
- [`toLocaleString()`](/javascript-object-prototype-tolocalestring/)
- [`toString()`](/javascript-object-prototype-tostring/)
- [`valueOf()`](/javascript-object-prototype-valueof/)
