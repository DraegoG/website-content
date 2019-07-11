---
title: "The Object getOwnPropertyNames() method"
description: "Find out all about the JavaScript getOwnPropertyNames() method of the Object object"
date: 2019-04-05T07:00:00+02:00
tags: js
---

`Object.getOwnPropertyNames()` returns an array containing all the names of the _own_ properties of the object passed as argument, including non-enumerable properties. It does not consider inherited properties.

Non enumerable properties are not iterated upon. Not listed in for..of loops, for example.

To get only a list of the enumerable properties you can use [`Object.keys()`](/javascript-object-keys/) instead.

Example:

```js
const dog = {}
dog.breed = 'Siberian Husky'
dog.name = 'Roger'

Object.getOwnPropertyNames(dog) //[ 'breed', 'name' ]
```