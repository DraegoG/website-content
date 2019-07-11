---
title: JavaScript Symbols
seotitle: A JavaScript Symbols Tutorial
description: "An easy to follow tutorial to understand JavaScript Symbols"
date: 2019-07-26T07:00:00+02:00
tags: js
---

Symbol is a primitive data type of JavaScript, along with [string](/javascript-string/), [number](/javascript-number/), boolean, null and undefined.

It was introduced in [ECMAScript 2015](/es6/), so just a few years ago.

It's a very peculiar data type. Once you create a symbol, its value is kept private and for internal use.

All that remains after the creation is the symbol reference.

You create a symbol by calling the `Symbol()` global factory function:

```js
const mySymbol = Symbol()
```

Every time you invoke `Symbol()` we get a new and unique symbol, guaranteed to be different from all other symbols:

```js
Symbol() === Symbol() //false
```

You can pass a parameter to `Symbol()`, and that is used as the symbol _description_, useful just for debugging purposes:

```js
console.log(Symbol()) //Symbol()
console.log(Symbol('Some Test')) //Symbol(Some Test)
```

Symbols are often used to identify object properties.

Often to avoid name clashing between properties, since no symbol is equal to another.

Or to add properties that the user cannot overwrite, intentionally or without realizing.

Examples:

```js
const NAME = Symbol()
const person = {
  [NAME]: 'Flavio'
}

person[NAME] //'Flavio'

const RUN = Symbol()
person[RUN] = () => 'Person is running'
console.log(person[RUN]()) //'Person is running'
```

Symbols are not enumerated, which means that they do not get included in a [`for..of` or `for..in` loop](/javascript-loops/) ran upon an object.

Symbols are not part of the [`Object.keys()`](/javascript-object-keys/) or [`Object.getOwnPropertyNames()`](/javascript-object-getownpropertynames/) result.

You can access all the symbols assigned to an object using the [`Object.getOwnPropertySymbols()`](/javascript-object-getownpropertysymbols/) method.
