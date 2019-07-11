---
title: "The Object create() method"
description: "Find out all about the JavaScript create() method of the Object object"
date: 2019-03-29T07:00:00+02:00
tags: js
---

Introduced in ES5.

Creates a new object, with the specified prototype.

Usage:

```js
const newObject = Object.create(prototype)
```

Example:

```js
const animal = {}
const dog = Object.create(animal)
```

The newly create object will inherit all the prototyope object properties.

You can specify a second parameter to add new properties to the object, that the prototype lacked:

```js
const newObject = Object.create(prototype, newProperties)
```

where newProperties is an object of objects that define each property.

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

I didn't just say `breed: 'Siberian Husky'` but I had to pass a property descriptor object, defined at the beginning of this page.

`Object.create()` is often used in combination with [`Object.assign()`](/javascript-object-assign/):

```js
const dog = Object.assign(Object.create(animal), {
  bark() {
    console.log('bark')
  }
})
```