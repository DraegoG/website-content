---
title: "The Set JavaScript Data Structure"
description: "A Set data structure allows to add data to a container, a collection of objects or primitive types (strings, numbers or booleans), and you can think of it as a Map where values are used as map keys, with the map value always being a boolean true."
date: 2018-03-03T09:06:29+02:00
updated: 2019-01-27T09:06:29+02:00
booktitle: "The Set Data Structure"
tags: js
tags_weight: 22
---

<!-- TOC -->

- [What is a Set](#what-is-a-set)
- [Initialize a Set](#initialize-a-set)
  - [Add items to a Set](#add-items-to-a-set)
  - [Check if an item is in the set](#check-if-an-item-is-in-the-set)
  - [Delete an item from a Set by key](#delete-an-item-from-a-set-by-key)
  - [Determine the number of items in a Set](#determine-the-number-of-items-in-a-set)
  - [Delete all items from a Set](#delete-all-items-from-a-set)
  - [Iterate the items in a Set](#iterate-the-items-in-a-set)
- [Initialize a Set with values](#initialize-a-set-with-values)
- [Convert to array](#convert-to-array)
  - [Convert the Set keys into an array](#convert-the-set-keys-into-an-array)
- [A WeakSet](#a-weakset)

<!-- /TOC -->

## What is a Set

A Set data structure allows to add data to a container.

[ECMAScript](/ecmascript/) 6 (also called ES2015) introduced the Set data structure to the [JavaScript](/javascript/) world, along with [Map](/javascript-data-structures-map/)

A Set is a collection of objects or primitive types (strings, numbers or booleans), and you can think of it as a Map where values are used as map keys, with the map value always being a boolean true.

## Initialize a Set

A Set is initialized by calling:

```js
const s = new Set()
```

### Add items to a Set

You can add items to the Set by using the `add` method:

```js
s.add('one')
s.add('two')
```

A set only stores unique elements, so calling `s.add('one')` multiple times won't add new items.

You can't add multiple elements to a set at the same time. You need to call `add()` multiple times.

### Check if an item is in the set

Once an element is in the set, we can check if the set contains it:

```js
s.has('one') //true
s.has('three') //false
```

### Delete an item from a Set by key

Use the `delete()` method:

```js
s.delete('one')
```

### Determine the number of items in a Set

Use the `size` property:

```js
s.size
```

### Delete all items from a Set

Use the `clear()` method:

```js
s.clear()
```

### Iterate the items in a Set

Use the `keys()` or `values()` methods - they are equivalent:

```js
for (const k of s.keys()) {
  console.log(k)
}

for (const k of s.values()) {
  console.log(k)
}
```

The `entries()` method returns an iterator, which you can use like this:

```js
const i = s.entries()
console.log(i.next())
```

calling `i.next()` will return each element as a `{ value, done = false }` object until the iterator ends, at which point `done` is `true`.

You can also use the forEach() method on the set:

```js
s.forEach(v => console.log(v))
```

or you can just use the set in a for..of loop:

```js
for (const k of s) {
  console.log(k)
}
```

## Initialize a Set with values

You can initialize a Set with a set of values:

```js
const s = new Set([1, 2, 3, 4])
```

## Convert to array

### Convert the Set keys into an array

```js
const a = [...s.keys()]

// or

const a = [...s.values()]
```

## A WeakSet

A WeakSet is a special kind of Set.

In a Set, items are never garbage collected. A WeakSet instead lets all its items be freely garbage collected. Every key of a WeakSet is an object. When the reference to this object is lost, the value can be garbage collected.

Here are the main differences:

1.  you cannot iterate over the WeakSet
2.  you cannot clear all items from a WeakSet
3.  you cannot check its size

A WeakSet is generally used by framework-level code, and only exposes these methods:

- add()
- has()
- delete()
