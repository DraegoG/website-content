---
title: "The Object getOwnPropertyDescriptor() method"
description: "Find out all about the JavaScript getOwnPropertyDescriptor() method of the Object object"
date: 2019-04-03T07:00:00+02:00
tags: js
---

This method can be used to retrieve the descriptor of a specific property.

Usage:

```js
const propertyDescriptor = Object.getOwnPropertyDescriptor(object, propertyName)
```

Example:

```js
const dog = {}
Object.defineProperties(dog, {
  breed: {
    value: 'Siberian Husky'
  }
})
Object.getOwnPropertyDescriptor(dog, 'breed')
/*
{
  value: 'Siberian Husky',
  writable: false,
  enumerable: false,
  configurable: false
}
*/
```