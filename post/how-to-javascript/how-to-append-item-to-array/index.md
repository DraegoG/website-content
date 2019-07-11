---
title: "How to append an item to an array in JavaScript"
date: 2018-05-25T07:06:15+02:00
description: "Find out the ways JavaScript offers you to append an item to an array, and the canonical way you should use"
tags: js
so: true
---

## Append a single item

To append a single item to an array, use the [`push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) method provided by the Array object:

```js
const fruits = ['banana', 'pear', 'apple']
fruits.push('mango')
```

`push()` mutates the original array.

To create a new array instead, use the [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) Array method:

```js
const fruits = ['banana', 'pear', 'apple']
const allfruits = fruits.concat('mango')
```

Notice that `concat()` does not actually add an item to the array, but creates a new array, which you can assign to another variable, or reassign to the original array (declaring it as `let`, as you cannot reassign a `const`):

```js
let fruits = ['banana', 'pear', 'apple']
fruits = fruits.concat('mango')
```

## Append multiple items

To append a multiple item to an array, you can use [`push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) by calling it with multiple arguments:

```js
const fruits = ['banana', 'pear', 'apple']
fruits.push('mango', 'melon', 'avocado')
```

You can also use the [`concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) method you saw before, passing a list of items separated by a comma:

```js
const fruits = ['banana', 'pear', 'apple']
const allfruits = fruits.concat('mango', 'melon', 'avocado')
```

or an array:

```js
const fruits = ['banana', 'pear', 'apple']
const allfruits = fruits.concat(['mango', 'melon', 'avocado'])
```

Remember that as described previously this method does not mutate the original array, but it  returns a new array.
