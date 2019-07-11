---
title: "The Object getOwnPropertyDescriptors() method"
description: "Find out all about the JavaScript getOwnPropertyDescriptors() method of the Object object"
date: 2019-04-04T07:00:00+02:00
tags: js
---

This method returns all own (non-inherited) properties descriptors of an object.

`Object.getOwnPropertyDescriptors(obj)` accepts an object, and returns a new object that provides a list of the descriptors.

Example:

```js
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
Object.getOwnPropertyDescriptors(dog)
/*
{
  breed: {
    value: 'Siberian Husky',
    writable: false,
    enumerable: false,
    configurable: false
  }
}
*/
```

There is one use case that makes this property very useful. ES2015 gave us `Object.assign()`, which copies all enumerable own properties from one or more objects, and return a new object. However there is a problem with that, because it does not correctly copies properties with non-default attributes.

If an object for example has just a setter, it's not correctly copied to a new object, using `Object.assign()`. For example with this object:

```js
const person1 = {
  set name(newName) {
    console.log(newName)
  }
}
```

This copy attempt won't work:

```js
const person2 = {}
Object.assign(person2, person1)
```

But this will work and copy over the setter correctly:

```js
const person3 = {}
Object.defineProperties(person3,
  Object.getOwnPropertyDescriptors(person1))
```

As you can see with a console test:

```js
person1.name = 'x'
"x"

person2.name = 'x'

person3.name = 'x'
"x"
```

`person2` misses the setter, it was not copied over.

The same limitation goes for shallow cloning objects with [`Object.create()`](/javascript-object-create/).
