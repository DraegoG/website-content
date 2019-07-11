---
title: The ES2017 Guide
description: "ECMAScript is the standard upon which JavaScript is based, and it's often abbreviated to ES. Discover everything about ECMAScript, and the features added in ES2017, aka ES8"
date: 2018-10-02T15:00:00+02:00
tags: js
tags_weight: 3
---

<!-- TOC -->

- [String padding](#string-padding)
- [Object.values()](#objectvalues)
- [Object.entries()](#objectentries)
- [getOwnPropertyDescriptors()](#getownpropertydescriptors)
  - [In what way is this useful?](#in-what-way-is-this-useful)
- [Trailing commas](#trailing-commas)
- [Async functions](#async-functions)
  - [Why they are useful](#why-they-are-useful)
  - [A quick example](#a-quick-example)
  - [Multiple async functions in series](#multiple-async-functions-in-series)
- [Shared Memory and Atomics](#shared-memory-and-atomics)

<!-- /TOC -->

ECMAScript 2017, edition 8 of the ECMA-262 Standard (also commonly called **ES2017** or **ES8**), was finalized in June 2017.

Compared to ES6, ES8 is a tiny release for JavaScript, but still it introduces very useful features:

- String padding
- `Object.values()`
- `Object.entries()`
- [`Object.getOwnPropertyDescriptors()`](/javascript-object-getownpropertydescriptors/)
- Trailing commas in function parameter lists and calls
- Async functions
- Shared memory and atomics

## String padding

The purpose of string padding is to **add characters to a string**, so it **reaches a specific length**.

ES2017 introduces two `String` methods: `padStart()` and `padEnd()`.

```js
padStart(targetLength [, padString])
padEnd(targetLength [, padString])
```

Sample usage:

| padStart()                  |              |
| --------------------------- |:-------------|
| 'test'.padStart(4)          | 'test'       |
| 'test'.padStart(5)          | '&nbsp;test'      |
| 'test'.padStart(8)          | '&nbsp;&nbsp;&nbsp;&nbsp;test'   |
| 'test'.padStart(8, 'abcd')  | 'abcdtest'   |


| padEnd()                  |              |
| ------------------------- |:-------------|
| 'test'.padEnd(4)          | 'test'       |
| 'test'.padEnd(5)          | 'test&nbsp;'      |
| 'test'.padEnd(8)          | 'test&nbsp;&nbsp;&nbsp;&nbsp;'   |
| 'test'.padEnd(8, 'abcd')  | 'testabcd'   |


## Object.values()

This method returns an array containing all the object own property values.

Usage:

```js
const person = { name: 'Fred', age: 87 }
Object.values(person) // ['Fred', 87]
```

`Object.values()` also works with arrays:

```js
const people = ['Fred', 'Tony']
Object.values(people) // ['Fred', 'Tony']
```

## Object.entries()

This method returns an array containing all the object own properties, as an array of `[key, value]` pairs.

Usage:

```js
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
```

[`Object.entries()`](/javascript-object-entries/) also works with arrays:

```js
const people = ['Fred', 'Tony']
Object.entries(people) // [['0', 'Fred'], ['1', 'Tony']]
```

## getOwnPropertyDescriptors()

This method returns all own (non-inherited) properties descriptors of an object.

Any object in JavaScript has a set of properties, and each of these properties has a descriptor.

A descriptor is a set of attributes of a property, and it's composed by a subset of the following:

- **value**: the value of the property
- **writable**: true the property can be changed
- **get**: a getter function for the property, called when the property is read
- **set**: a setter function for the property, called when the property is set to a value
- **configurable**: if false, the property cannot be removed nor any attribute can be changed, except its value
- **enumerable**: true if the property is enumerable

`Object.getOwnPropertyDescriptors(obj)` accepts an object, and returns an object with the set of descriptors.

### In what way is this useful?

ES6 gave us [`Object.assign()`](/javascript-object-assign/), which copies all enumerable own properties from one or more objects, and return a new object.

However there is a problem with that, because it does not correctly copies properties with non-default attributes.

If an object for example has just a setter, it's not correctly copied to a new object, using `Object.assign()`.

For example with

```js
const person1 = {
    set name(newName) {
        console.log(newName)
    }
}
```

This won't work:

```js
const person2 = {}
Object.assign(person2, person1)
```

But this will work:

```js
const person3 = {}
Object.defineProperties(person3,
  Object.getOwnPropertyDescriptors(person1))
```

As you can see with a simple console test:

```js
person1.name = 'x'
"x"

person2.name = 'x'

person3.name = 'x'
"x"
```

`person2` misses the setter, it was not copied over.

The same limitation goes for shallow cloning objects with [`Object.create()`](/javascript-object-create/).

## Trailing commas

This feature allows to have trailing commas in function declarations, and in functions calls:

```js
const doSomething = (var1, var2,) => {
  //...
}

doSomething('test2', 'test2',)
```

This change will encourage developers to stop the ugly "comma at the start of the line" habit.

## Async functions

> Check the dedicated post about [async/await](/javascript-async-await/)

ES2017 introduced the concept of **async functions**, and it's the most important change introduced in this ECMAScript edition.

Async functions are a combination of promises and generators to reduce the boilerplate around promises, and the "don't break the chain" limitation of chaining promises.

### Why they are useful

It's a higher level abstraction over promises.

When Promises were introduced in ES6, they were meant to solve a problem with asynchronous code, and they did, but over the 2 years that separated ES6 and ES2017, it was clear that _promises could not be the final solution_.
Promises were introduced to solve the famous _callback hell_ problem, but they introduced complexity on their own, and syntax complexity.
They were good primitives around which a better syntax could be exposed to the developers: enter **async functions**.

### A quick example

Code making use of asynchronous functions can be written as

```js
function doSomethingAsync() {
    return new Promise((resolve) => {
        setTimeout(() => resolve('I did something'), 3000)
    })
}

async function doSomething() {
    console.log(await doSomethingAsync())
}

console.log('Before')
doSomething()
console.log('After')
```

The above code will print the following to the browser console:

```
Before
After
I did something //after 3s
```

### Multiple async functions in series

Async functions can be chained very easily, and the syntax is much more readable than with plain promises:

```js
function promiseToDoSomething() {
    return new Promise((resolve)=>{
        setTimeout(() => resolve('I did something'), 10000)
    })
}

async function watchOverSomeoneDoingSomething() {
    const something = await promiseToDoSomething()
    return something + ' and I watched'
}

async function watchOverSomeoneWatchingSomeoneDoingSomething() {
    const something = await watchOverSomeoneDoingSomething()
    return something + ' and I watched as well'
}

watchOverSomeoneWatchingSomeoneDoingSomething().then((res) => {
    console.log(res)
})
```

## Shared Memory and Atomics

WebWorkers are used to create multithreaded programs in the browser.

They offer a messaging protocol via events. Since ES2017, you can create a shared memory array between [web workers](/web-workers/) and their creator, using a `SharedArrayBuffer`.

Since it's unknown how much time writing to a shared memory portion takes to propagate, **Atomics** are a way to enforce that when reading a value, any kind of writing operation is completed.

Any more detail on this [can be found in the spec proposal](https://github.com/tc39/ecmascript_sharedmem/blob/master/TUTORIAL.md), which has since been implemented.
