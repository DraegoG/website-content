---
title: Destructuring Objects and Arrays in JavaScript
description: "Learn how to use the destructuring syntax to work with arrays and objects in JavaScript"
date: 2019-01-04T07:00:00+02:00
tags: js
---

Given an object, using the destructuring syntax you can extract just some values and put them into named variables:

```js
const person = {
  firstName: 'Tom',
  lastName: 'Cruise',
  actor: true,
  age: 54 //made up
}

const { firstName: name, age } = person //name: Tom, age: 54
```

`name` and `age` contain the desired values.

The syntax also works on arrays:

```js
const a = [1, 2, 3, 4, 5]
const [first, second] = a
```

This statement creates 3 new variables by getting the items with index 0, 1, 4 from the array `a`:

```js
const [first, second, , , fifth] = a
```
