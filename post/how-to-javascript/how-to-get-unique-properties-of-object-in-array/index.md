---
title: "How to get the unique properties of a set of objects in a JavaScript array"
date: 2018-09-28T07:00:00+02:00
description: "Given an array of objects, here's what you can do if you want to get the values of a property, but not duplicated."
tags: js
---

Suppose you have a bills array with this content:

```js
const bills = [
  { date: '2018-01-20', amount: '220', category: 'Electricity' },
  { date: '2018-01-20', amount: '20', category: 'Gas' },
  { date: '2018-02-20', amount: '120', category: 'Electricity' }
]
```

and you want to extract the unique values of the `category` attribute of each item in the array.

Here's what you can do:

```js
const categories = [...new Set(bills.map(bill => bill.category))]
```

## Explanation

[Set](/javascript-data-structures-set/) is a new data structure that JavaScript got in [ES6](/es6/). It's a collection of unique values. We put into that the list of property values we get from using `map()`, which how we used it will return this array:

```js
['Electricity', 'Gas', 'Electricity']
```

Passing through Set, we'll remove the duplicates.

`...` is the [**spread operator**](/javascript-spread-operator/), which will expand the set values into an array.