---
title: JavaScript Property Descriptors
description: "An explanation of property descriptors and what they are useful for"
date: 2019-03-27T07:07:09+02:00
tags: js
---

Any object in JavaScript has a set of properties, and each of these properties has a **descriptor**.

This is an object that defines a property behavior and own properties.

Many Object static methods interact with it. Those methods include:

- [`Object.create()`](/javascript-object-create/)
- [`Object.defineProperties()`](/javascript-object-defineproperties/)
- [`Object.defineProperty()`](/javascript-object-defineproperty/)
- [`Object.getOwnPropertyDescriptor()`](/javascript-object-getownpropertydescriptor/)
- [`Object.getOwnPropertyDescriptors()`](/javascript-object-getownpropertydescriptors/)

Here is an example of a property descriptor object:

```js
{
  value: 'Something'
}
```

This is the simplest one. `value` is the property value, in a key-value definition. This `key` is defined as the object key, when you define this property in an object:

```js
{
  breed: {
    value: 'Siberian Husky'
  }
}
```

Example:

```js
const animal = {}
const dog = Object.create(animal, {
  breed: {
    value: 'Siberian Husky'
  }
});
console.log(dog.breed) //'Siberian Husky'
```

You can pass additional properties to define each different object property:

- **value**: the value of the property
- **writable**: true the property can be changed
- **configurable**: if false, the property cannot be removed nor any attribute can be changed, except its value
- **enumerable**: true if the property is enumerable
- **get**: a getter function for the property, called when the property is read
- **set**: a setter function for the property, called when the property is set to a value

`writable`, `configurable` and `enumerable` set the behavior of that property. They have a boolean value, and by default those are all `false`.

Example:

```js
const animal = {}
const dog = Object.create(animal, {
  breed: {
    value: 'Siberian Husky',
    writable: false
  }
});
console.log(dog.breed) //'Siberian Husky'
dog.breed = 'Pug' //TypeError: Cannot assign to read only property 'breed' of object '#<Object>'
```
