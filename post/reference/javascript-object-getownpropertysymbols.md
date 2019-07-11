---
title: "The Object getOwnPropertySymbols() method"
description: "Find out all about the JavaScript getOwnPropertySymbols() method of the Object object"
date: 2019-04-06T07:00:00+02:00
tags: js
---

Get an array of symbols defined on an object.

Symbols is an ES2015 feature, and this method was introduced in ES2015 as well.

Example:

```js
const dog = {}
const r = Symbol('Roger')
const s = Symbol('Syd')
dog[r] = {
  name: 'Roger',
  age: 6
}
dog[s] = {
  name: 'Syd',
  age: 5
}

Object.getOwnPropertySymbols(dog) //[ Symbol(Roger), Symbol(Syd) ]
```