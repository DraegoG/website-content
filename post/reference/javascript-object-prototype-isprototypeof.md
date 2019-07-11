---
title: "The Object isPrototypeOf() method"
description: "Find out all about the JavaScript isPrototypeOf() method of an object"
date: 2019-04-18T07:00:00+02:00
tags: js
---

Called on an object instance, accepts an object as argument. If the object you called `isPrototypeOf()` on appears in the prototype chain of the object passed as argument, it returns `true`. Otherwise it returns `false`.

Example:

```js
const Animal = {
  isAnimal: true
}

const Mammal = Object.create(Animal)
Mammal.isMammal = true

Animal.isPrototypeOf(Mammal) //true

const dog = Object.create(Animal)
Object.setPrototypeOf(dog, Mammal)

Animal.isPrototypeOf(dog) //true
Mammal.isPrototypeOf(dog) //true
```