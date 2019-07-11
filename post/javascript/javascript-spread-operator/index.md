---
title: The JavaScript Spread Operator
date: 2019-06-08T07:00:00+02:00
description: "Learn the basics of the JavaScript Spread Operator"
tags: js
---

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
const f = (foo, bar) => {}
const a = [1, 2]
f(...a)
```

The **rest element** is useful when working with **array destructuring**:

```js
const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
```

and **spread elements**:

```js
const numbers = [1, 2, 3, 4, 5]
const sum = (a, b, c, d, e) => a + b + c + d + e
const result = sum(...numbers)
```

ES2018 introduces rest properties, which are the same but for objects.

**Rest properties**:

```js
const { first, second, ...others } = {
  first: 1,
  second: 2,
  third: 3,
  fourth: 4,
  fifth: 5
}

first // 1
second // 2
others // { third: 3, fourth: 4, fifth: 5 }
```

**Spread properties** allow to create a new object by combining the properties of the object passed after the spread operator:

```js
const items = { first, second, ...others }
items //{ first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }
```

It is also the perfect way to merge two simple objects into one:

```js
const object1 = {
  name: 'Flavio'
}

const object2 = {
  age: 35
}

const object3 = {...object1, ...object2 }
```
