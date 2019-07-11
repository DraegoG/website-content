---
title: "The Object setPrototypeOf() method"
description: "Find out all about the JavaScript setPrototypeOf() method of the Object object"
date: 2019-04-15T07:00:00+02:00
tags: js
---

Set the prototype of an object.

> While you're here, see my guide on [JavaScript Prototypal Inheritance](/javascript-prototypal-inheritance/)

Accepts two arguments: the object and the prototype.

Usage:

```js
Object.setPrototypeOf(object, prototype)
```

Example:

```js
const Animal = {}
Animal.isAnimal = true

const Mammal = Object.create(Animal)
Mammal.isMammal = true

console.log('-------')
Mammal.isAnimal //true

const dog = Object.create(Animal)

dog.isAnimal  //true
console.log(dog.isMammal)  //undefined

Object.setPrototypeOf(dog, Mammal)

console.log(dog.isAnimal) //true
console.log(dog.isMammal) //true
```