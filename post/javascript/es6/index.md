---
title: The ES6 Guide
description: "ECMAScript is the standard upon which JavaScript is based, and it's often abbreviated to ES. Discover everything about ECMAScript, and the features added in ES6, aka ES2015."
date: 2018-09-30T07:00:00+02:00
updated: 2019-02-04T07:00:00+02:00
tags: js
tags_weight: 3
---

<!-- TOC -->

- [Arrow Functions](#arrow-functions)
- [A new `this` scope](#a-new-this-scope)
- [Promises](#promises)
- [Generators](#generators)
- [`let` and `const`](#let-and-const)
- [Classes](#classes)
  - [Constructor](#constructor)
  - [Super](#super)
  - [Getters and setters](#getters-and-setters)
- [Modules](#modules)
  - [Importing modules](#importing-modules)
  - [Exporting modules](#exporting-modules)
- [Template Literals](#template-literals)
- [Default parameters](#default-parameters)
- [The spread operator](#the-spread-operator)
- [Destructuring assignments](#destructuring-assignments)
- [Enhanced Object Literals](#enhanced-object-literals)
  - [Simpler syntax to include variables](#simpler-syntax-to-include-variables)
  - [Prototype](#prototype)
  - [super()](#super)
  - [Dynamic properties](#dynamic-properties)
- [For-of loop](#for-of-loop)
- [Map and Set](#map-and-set)
- [New String methods](#new-string-methods)
- [New Object methods](#new-object-methods)

<!-- /TOC -->

ECMAScript 2015, also known as ES6, is a fundamental version of the ECMAScript standard.

**Published 4 years after the latest standard revision**, ECMAScript 5.1, it also marked the switch from edition number to year number.

So **it should not be named as ES6** (although everyone calls it as such) but ES2015 instead.

> ES5 was 10 years in the making, from 1999 to 2009, and as such it was also a fundamental and very important revision of the language, but now much time has passed that it's not worth discussing how pre-ES5 code worked.

Since this long time passed between ES5.1 and ES6, the release is full of important new features and major changes in suggested best practices in developing JavaScript programs. To understand how fundamental ES2015 is, just keep in mind that with this version, the specification document went from 250 pages to ~600.

This article describes the most important changes.

## Arrow Functions

Arrow functions since their introduction changed how most JavaScript code looks (and works).

Visually, it's a simple and welcome change, from:

```js
const something = function something() {
  //...
}
```

to

```js
const something = () => {
  //...
}
```

And if the function body is a one-liner, just:

```js
const something = () => doSomething()
```

Also, if you have a single parameter, you could write:

```js
const something = param => doSomething(param)
```

This is not a breaking change, regular `function`s will continue to work just as before.

## A new `this` scope

The `this` scope with arrow functions is inherited from the context.

With regular `function`s `this` always refers to the nearest function, while with arrow functions this problem is removed, and you won't need to write `var that = this` ever again.

## Promises

Promises (check the [full guide to promises](/javascript-promises/)) allow us to eliminate the famous "callback hell", although they introduce a bit more complexity (which has been solved in ES2017 with `async`, a higher level construct).

Promises have been used by JavaScript developers well before ES2015, with many different libraries implementations (e.g. jQuery, q, deferred.js, vow...), and the standard put a common ground across differences.

By using promises you can rewrite this code

```js
setTimeout(function() {
  console.log('I promised to run after 1s')
  setTimeout(function() {
    console.log('I promised to run after 2s')
  }, 1000)
}, 1000)
```

as

```js
const wait = () => new Promise((resolve, reject) => {
  setTimeout(resolve, 1000)
})

wait().then(() => {
  console.log('I promised to run after 1s')
  return wait()
})
.then(() => console.log('I promised to run after 2s'))
```

## Generators

Generators are a special kind of function with the ability to pause itself, and resume later, allowing other code to run in the meantime.

See the full [JavaScript Generators](/javascript-generators/) Guide for a detailed explanation of the topic.

## `let` and `const`

`var` is traditionally **function scoped**.

`let` is a new variable declaration which is **block scoped**.

This means that declaring `let` variables in a for loop, inside an if or in a plain block is not going to let that variable "escape" the block, while `var`s are hoisted up to the function definition.

`const` is just like `let`, but **immutable**.

In JavaScript moving forward, you'll see little to no `var` declarations any more, just `let` and `const`.

`const` in particular, maybe surprisingly, is **very widely used** nowadays with immutability being very popular.

## Classes

Traditionally JavaScript is the only mainstream language with prototype-based inheritance. Programmers switching to JS from class-based language found it puzzling, but ES2015 introduced classes, which are just syntactic sugar over the inner working, but changed a lot how we build JavaScript programs.

Now inheritance is very easy and resembles other object-oriented programming languages:

```js
class Person {
  constructor(name) {
    this.name = name
  }

  hello() {
    return 'Hello, I am ' + this.name + '.'
  }
}

class Actor extends Person {
  hello() {
    return super.hello() + ' I am an actor.'
  }
}

var tomCruise = new Actor('Tom Cruise')
tomCruise.hello()
```

(the above program prints "_Hello, I am Tom Cruise. I am an actor._")

Classes do not have explicit class variable declarations, but you must initialize any variable in the constructor.

### Constructor

Classes have a special method called `constructor` which is called when a class is initialized via `new`.

### Super

The parent class can be referenced using `super()`.

### Getters and setters

A getter for a property can be declared as

```js
class Person {
  get fullName() {
    return `${this.firstName} ${this.lastName}`
  }
}
```

Setters are written in the same way:

```js
class Person {
  set age(years) {
    this.theAge = years
  }
}
```

## Modules

Before ES2015, there were at least 3 major modules competing standards, which fragmented the community:

- AMD
- RequireJS
- CommonJS

ES2015 standardized these into a common format.

### Importing modules

Importing is done via the `import ... from ...` construct:

```js
import * from 'mymodule'
import React from 'react'
import { React, Component } from 'react'
import React as MyLibrary from 'react'
```

### Exporting modules

You can write modules and export anything to other modules using the `export` keyword:

```js
export var number = 2
export function bar() { /* ... */ }
```

## Template Literals

Template literals are a new syntax to create strings:

```js
const aString = `A string`
```

They provide a way to embed expressions into strings, effectively inserting the values, by using the `${a_variable}` syntax:

```js
const joe = 'test'
const string = `something ${joe}` //something test
```

You can perform more complex expressions as well:

```js
const string = `something ${1 + 2 + 3}`
const string2 = `something ${doSomething() ? 'x' : 'y' }`
```

and strings can span over multiple lines:

```js
const string3 = `Hey
this

string
is awesome!`
```

Compare how we used to do multiline strings pre-ES2015:

```js
var str = 'One\n' +
'Two\n' +
'Three'
```

> [See this post for an in-depth guide on template literals
](/javascript-template-literals/)

## Default parameters

Functions now support default parameters:

```js
const someFunction = function(index = 0, testing = true) { /* ... */ }
someFunction()
```

## The spread operator

You can expand an array, an object or a string using the spread operator `...`.

Let's start with an array example. Given

```js
const a = [1, 2, 3]
```

you can create a new array using

```js
const b = [...a, 4, 5, 6]
```

You can also create a copy of an array using

```js
const c = [...a]
```

This works for objects as well. Clone an object with:

```js
const newObj = { ...oldObj }
```

Using strings, the spread operator creates an array with each char in the string:

```js
const hey = 'hey'
const arrayized = [...hey] // ['h', 'e', 'y']
```

This operator has some pretty useful applications. The most important one is the ability to use an array as function argument in a very simple way:

```js
const f = (arg1, arg2) => {}
const a = [1, 2]
f(...a)
```

(in the past you could do this using `f.apply(null, a)` but that's not as nice and readable)

## Destructuring assignments

Given an object, you can extract just some values and put them into named variables:

```js
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54, //made up
}

const {firstName: name, age} = person
```

`name` and `age` contain the desired values.

The syntax also works on arrays:

```js
const a = [1,2,3,4,5]
const [first, second] = a
```

This statement creates 3 new variables by getting the items with index 0, 1, 4 from the array `a`:

```js
const [first, second, , , fifth] = a
```

## Enhanced Object Literals

In ES2015 Object Literals gained superpowers.

### Simpler syntax to include variables

Instead of doing

```js
const something = 'y'
const x = {
  something: something
}
```

you can do

```js
const something = 'y'
const x = {
  something
}
```

### Prototype

A prototype can be specified with

```js
const anObject = { y: 'y' }
const x = {
  __proto__: anObject
}
```

### super()

```js
const anObject = { y: 'y', test: () => 'zoo' }
const x = {
  __proto__: anObject,
  test() {
    return super.test() + 'x'
  }
}
x.test() //zoox
```

### Dynamic properties

```js
const x = {
  ['a' + '_' + 'b']: 'z'
}
x.a_b //z
```

## For-of loop

ES5 back in 2009 introduced `forEach()` loops. While nice, they offered no way to break, like `for` loops always did.

ES2015 introduced the **`for-of` loop**, which combines the conciseness of `forEach` with the ability to break:

```js
//iterate over the value
for (const v of ['a', 'b', 'c']) {
  console.log(v);
}

//get the index as well, using `entries()`
for (const [i, v] of ['a', 'b', 'c'].entries()) {
  console.log(i, v);
}
```

## Map and Set

[**Map**](/javascript-data-structures-map/) and [**Set**](/javascript-data-structures-set/) (and their respective garbage collected **WeakMap** and **WeakSet**) are the official implementations of two very popular data structures.

## New String methods

Any string value got some new instance methods:

- `repeat()` repeats the strings for the specificed number of times: `'Ho'.repeat(3) //HoHoHo`
- `codePointAt()` handles retrieving the Unicode code of characters that cannot be represented by a single 16-bit UTF-16 unit, but need 2 instead

## New Object methods

ES6 introduced several static methods under the Object namespace:

- [`Object.is()`](/javascript-object-is/) determines if two values are the same value
- [`Object.assign()`](/javascript-object-assign/) used to shallow copy an object
- `Object.setPrototypeOf` sets an object prototype