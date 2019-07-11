---
title: "React Concept: Immutability"
date: 2018-12-15T07:00:00+02:00
description: "What is immutability? And how does it fit in the React world?"
tags: react
---

One concept you will likely meet when programming in React is immutability (and its opposite, mutability).

It's a controversial topic, but whatever you might think about the concept of immutability, React and most of its ecosystem kind of forces this, so you need to at least have a grasp of why it's so important and the implications of it.

In programming, a variable is immutable when its value cannot change after it's created.

You are already using immutable variables without knowing it when you manipulate a string. Strings are immutable by default, when you change them in reality you create a new string and assign it to the same variable name.

An immutable variable can never be changed. To update its value, you create a new variable.

The same applies to objects and arrays.

Instead of changing an array, to add a new item you create a new array by concatenating the old array, plus the new item.

An object is never updated, but copied before changing it.

This applies to React in many places.

For example, you should never mutate the `state` property of a component directly, but only through the `setState()` method.

In Redux, you never mutate the state directly, but only through reducers, which are functions.

The question is, why?

There are various reasons, the most important of which are:

- Mutations can be centralized, like in the case of Redux, which improves your debugging capabilities and reduces sources of errors.
- Code looks cleaner and simpler to understand. You never expect a function to change some value without you knowing, which gives you **predictability**. When a function does not mutate objects but just returns a new object, it's called a pure function.
- The library can optimize the code because for example JavaScript is faster when swapping an old object reference for an entirely new object, rather than mutating an existing object. This gives you **performance**.
