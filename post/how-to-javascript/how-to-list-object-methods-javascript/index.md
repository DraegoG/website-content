---
title: "How to list all methods of an object in JavaScript"
date: 2019-02-04T07:00:00+02:00
description: "Find out how to get an array with a JavaScript object methods"
tags: js
---

We can use the [`Object.getOwnPropertyNames()`](/javascript-object-getownpropertynames/) function to get all the property names linked to an object.

Then we can filter the resulting array, to only include that property name if it's a function.

We determine if it's a function by using `typeof` on it.

For example here is how we might create a utility function to do what we need:

```js
getMethods = (obj) => Object.getOwnPropertyNames(obj).filter(item => typeof obj[item] === 'function')
```

This lists only the methods defined on that specific object, not any method defined in its prototype chain.

To do that we must take a slightly different route. We must first iterate the prototype chain and we list all the properties in an array. Then we check if each single property is a function.

An easy way to make sure we don't duplicate methods as we navigate the prototype chain (like `constructor` which is always present), we use a Set data structure that makes sure values are unique:

```js
const getMethods = (obj) => {
  let properties = new Set()
  let currentObj = obj
  do {
    Object.getOwnPropertyNames(currentObj).map(item => properties.add(item))
  } while ((currentObj = Object.getPrototypeOf(currentObj)))
  return [...properties.keys()].filter(item => typeof obj[item] === 'function')
}
```

Example usage:

```js
getMethods("")
getMethods(new String('test'))
getMethods({})
getMethods(Date.prototype)
```