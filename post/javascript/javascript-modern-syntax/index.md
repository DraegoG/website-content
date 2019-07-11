---
title: A quick reference guide to Modern JavaScript Syntax
description: "Many times, code samples are using the latest JavaScript features available. Sometimes those features can be hard to be distinguished from a framework features. It happens frequently with React for example, which encourages a very modern approach to JavaScript."
date: 2018-07-03T07:00:00+02:00
booktitle: "Modern JavaScript Syntax"
tags: js
tags_weight: 41
---

Many times, code samples are using the latest JavaScript features available.

Sometimes those features can be hard to be distinguished from a framework features. It happens frequently with React for example, which encourages a very "modern" approach to JavaScript.

This post aims to explain all the little things that might trip you up, especially if you come from a pre-ES6 JavaScript background, or also if you're starting from zero.

The goal is to make you at least recognize which constructs are regular JavaScript, and which ones are part of a framework. I'm not going deep into explaining how those things work, and instead I'll give some pointers if you want to know more.

## Arrow functions

Arrow functions have this syntax:

```js
const myFunction = () => {
  //...
}
```

A bit different than regular functions:

```js
const myFunction = function() {
  //...
}
```

The () can host parameters, just like in regular functions. Sometimes the brackets are removed entirely when there's just one statement in the function, and that's an implicit return value (no return keyword needed):

```js
const myFunction = i => 3 * i
```

[More on Arrow Functions](/javascript-arrow-functions/)

## The spread operator

If you see

```js
const c = [...a]
```

This statement copies an array.

You can add items to an array as well, using

```js
const c = [...a, 2, 'test']
```

The `...` is called spread operator. You can use it on objects as well:

```js
const newObj = { ...oldObj } //shallow clone an object
```

> [More on the spread operator](/javascript-spread-operator/)

## Destructuring assignments

You can extract just _some_ properties from an object using this syntax:

```js
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54 //made up
}

const { firstName: name, age } = person
```

You will now have two const values `name` and `age`.

The syntax also works on arrays:

```js
const a = [1,2,3,4,5]
[first, second, , , fifth] = a
```

## Template literals

If you see strings enclosed in backticks, it's a template literal:

```js
const str = `test`
```

Inside this, you can put variables and execute javascript, using `${...}` snippets:

```js
const string = `something ${1 + 2 + 3}`
const string2 = `something ${doSomething() ? 'x' : 'y'}`
```

And also, you can span a string over multiple lines:

```js
const string3 = `Hey
this

string
is awesome!`
```
