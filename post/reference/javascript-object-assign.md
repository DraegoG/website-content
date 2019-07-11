---
title: "The Object assign() method"
description: "Find out all about the JavaScript assign() method of the Object object"
date: 2019-03-28T07:00:00+02:00
tags: js
---

Introduced in `ES2015`, this method copies all the **enumerable own properties** of one or more objects into another.

Its primary use case is to create a shallow copy of an object.

```js
const copied = Object.assign({}, original)
```

Being a shallow copy, values are cloned, and objects references are copied (not the objects themselves), so if you edit an object property in the original object, that's modified also in the copied object, since the referenced inner object is the same:

```js
const original = {
  name: 'Fiesta',
  car: {
    color: 'blue'
  }
}
const copied = Object.assign({}, original)

original.name = 'Focus'
original.car.color = 'yellow'

copied.name //Fiesta
copied.car.color //yellow
```

I mentioned "one or more":

```js
const wisePerson = {
  isWise: true
}
const foolishPerson = {
  isFoolish: true
}
const wiseAndFoolishPerson = Object.assign({}, wisePerson, foolishPerson)

console.log(wiseAndFoolishPerson) //{ isWise: true, isFoolish: true }
```
