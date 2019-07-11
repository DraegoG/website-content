---
title: The ES2019 Guide
description: "ECMAScript is the standard upon which JavaScript is based, and it's often abbreviated to ES. Discover everything about ECMAScript, and the features added in ES2019"
date: 2019-02-13T15:00:00+02:00
tags: js
---

ESNext is a name that always indicates the next version of JavaScript.

The current ECMAScript version is **ES2018**.
It was released in June 2018.

Historically JavaScript editions have been standardized during the summer, so we can expect **ECMAScript 2019** to be released in summer 2019.

So at the time of writing, ES2018 has been released, and **ESNext is ES2019**

Proposals to the ECMAScript standard are organized in stages. Stages 1-3 are an incubator of new features, and features reaching Stage 4 are finalized as part of the new standard.

At the time of writing we have a number of features at **Stage 4**. I will introduce them in this section. The latest versions of the major browsers should already implement most of those.

- `Array.prototype.{flat,flatMap}`
- Optional catch binding
- `Object.fromEntries()`
- `String.prototype.{trimStart,trimEnd}`
- `Symbol.prototype.description`
- JSON improvements
- Well-formed `JSON.stringify()`
- `Function.prototype.toString()`

Some of those changes are mostly for internal use, but it's also good to know what is going on.

There are other features at Stage 3, which might be promoted to Stage 4 in the next few months, and you can check them out on this GitHub repository: <https://github.com/tc39/proposals>.

## `Array.prototype.{flat,flatMap}`

`flat()` is a new array instance method that can create a one-dimensional array from a multidimensional array.

Example:

```js
['Dog', ['Sheep', 'Wolf']].flat()
//[ 'Dog', 'Sheep', 'Wolf' ]
```

By default it only "flats" up to one level, but you can add a parameter to set the number of levels you want to flat the array to. Set it to `Infinity` to have unlimited levels:

```js
['Dog', ['Sheep', ['Wolf']]].flat()
//[ 'Dog', 'Sheep', [ 'Wolf' ] ]

['Dog', ['Sheep', ['Wolf']]].flat(2)
//[ 'Dog', 'Sheep', 'Wolf' ]

['Dog', ['Sheep', ['Wolf']]].flat(Infinity)
//[ 'Dog', 'Sheep', 'Wolf' ]
```

If you are familiar with the JavaScript `map()` method of an array, you know that using it you can execute a function on every element of an array.

`flatMap()` is a new Array instance method that combines `flat()` with `map()`. It's useful when calling a function that returns an array in the map() callback, but you want your resulted array to be flat:

```js
['My dog', 'is awesome'].map(words => words.split(' '))
//[ [ 'My', 'dog' ], [ 'is', 'awesome' ] ]

['My dog', 'is awesome'].flatMap(words => words.split(' '))
//[ 'My', 'dog', 'is', 'awesome' ]
```

## Optional catch binding

Sometimes we dont need to have a parameter binded to the catch block of a try/catch.

We previously had to do:

```js
try {
  //...
} catch (e) {
  //handle error
}
```

Even if we never had to use `e` to analyze the error. We can now simply omit it:

```js
try {
  //...
} catch {
  //handle error
}
```

## `Object.fromEntries()`

Objects have an `entries()` method, since [ES2017](/es2017/).

It returns an array containing all the object own properties, as an array of `[key, value]` pairs:

```js
const person = { name: 'Fred', age: 87 }
Object.entries(person) // [['name', 'Fred'], ['age', 87]]
```

ES2019 introduces a new `Object.fromEntries()` method, which can create a new object from such array of properties:

```js
const person = { name: 'Fred', age: 87 }
const entries = Object.entries(person)
const newPerson = Object.fromEntries(entries)

person !== newPerson //true
```

## `String.prototype.{trimStart,trimEnd}`

This feature has been part of v8/Chrome for almost a year now, and it's going to be standardized in ES2019.

### `trimStart()`

Return a new string with removed white space from the start of the original string

```js
'Testing'.trimStart() //'Testing'
' Testing'.trimStart() //'Testing'
' Testing '.trimStart() //'Testing '
'Testing'.trimStart() //'Testing'
```

### `trimEnd()`

Return a new string with removed white space from the end of the original string

```js
'Testing'.trimEnd() //'Testing'
' Testing'.trimEnd() //' Testing'
' Testing '.trimEnd() //' Testing'
'Testing '.trimEnd() //'Testing'
```

## `Symbol.prototype.description`

You can now retrieve the description of a Symbol by accessing its `description` property instead of having to use the `toString()` method:

```js
const testSymbol = Symbol('Test')
testSymbol.description // 'Test'
```

## JSON improvements

Before this change, the line separator (\u2028) and paragraph separator (\u2029) symbols were not allowed in strings parsed as [JSON](/json/).

Using `JSON.parse()`, those characters resulted in a `SyntaxError` but now they parse correctly, as defined by the JSON standard.

## Well-formed `JSON.stringify()`

Fixes the `JSON.stringify()` output when it processes surrogate UTF-8 code points (U+D800 to U+DFFF).

Before this change calling `JSON.stringify()` would return a malformed Unicode character (a "�").

Now those surrogate code points can be safely represented as strings using `JSON.stringify()`, and transformed back into their original representation using `JSON.parse()`.

## `Function.prototype.toString()`

Functions have always had an instance method called `toString()` which return a string containing the function code.

ES2019 introduced a change to the return value to avoid stripping comments and other characters like whitespace, exactly representing the function as it was defined.

If previously we had:

```js
function /* this is bar */ bar () {}
```

The behavior was this:

```js
bar.toString() //'function bar() {}
```

now the new behavior is:

```js
bar.toString(); // 'function /* this is bar */ bar () {}'
```
