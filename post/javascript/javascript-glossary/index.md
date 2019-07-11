---
title: "The JavaScript Glossary"
description: "A guide to a few terms used in frontend development that might be alien to you"
date: 2018-04-21T06:06:29+02:00
booktitle: "Glossary"
tags: js
tags_weight: 39
---

<!-- TOC -->

- [Asynchronous](#asynchronous)
- [Block](#block)
- [Block Scoping](#block-scoping)
- [Callback](#callback)
- [Declarative](#declarative)
- [Fallback](#fallback)
- [Function Scoping](#function-scoping)
- [Immutability](#immutability)
- [Lexical Scoping](#lexical-scoping)
- [Polyfill](#polyfill)
- [Pure function](#pure-function)
- [Reassignment](#reassignment)
- [Scope](#scope)
- [Scoping](#scoping)
- [Shim](#shim)
- [Side effect](#side-effect)
- [State](#state)
- [Stateful](#stateful)
- [Stateless](#stateless)
- [Strict mode](#strict-mode)
- [Tree Shaking](#tree-shaking)

<!-- /TOC -->

## Asynchronous

Code is asynchronous when you initiate something, forget about it, and when the result is ready you get it back without having to wait for it.
The typical example is an AJAX call, which might take even seconds and in the meantime you complete other stuff, and when the response is ready, the callback function gets called. Promises and async/await are the modern way to handle async.

## Block

In JavaScript a block is delimited curly braces (`{}`). An `if` statement contains a block, a `for` loop contains a block.

## Block Scoping

With Function [Scoping](#scoping), any variable defined in a block is visible and accessible from inside the whole [block](#block), but not outside of it.

## Callback

A callback is a function that's invoked when something happens. A click event associated to an element has a callback function that's invoked when the user clicks the element. A fetch request has a callback that's called when the resource is downloaded.

## Declarative

A declarative approach is when you tell the machine what you need to do, and you let it figure out the details. React is considered declarative, as you reason about abstractions rather than editing the DOM directly. Every high level programming language is more declarative than a low level programming language like Assembler. JavaScript is more declarative than C. HTML is declarative.

## Fallback

A fallback is used to provide a good experience when a user hasn't access to a particular functionality. For example a user that browses with JavaScript disabled should be able to have a fallback to a plain HTML version of the page. Or for a browser that has not implemented an API, you should have a fallback to avoid completely breaking the experience of the user.

## Function Scoping

With Function [Scoping](#scoping), any variable defined in a function is visible and accessible from inside the whole function.

## Immutability

A variable is immutable when its value cannot change after it's created. A mutable variable can be changed. The same applies to objects and arrays.

## Lexical Scoping

Lexical [Scoping](#scoping) is a particular kind of scoping which means that the value of a variable is defined by its position when it's written. Not when it's called, which is something that happens with the alternative, _dynamic scoping_ (used in some other programming languages).

## Polyfill

A polyfill is a way to provide new functionality available in modern JavaScript or a modern browser API to older browsers. A polyfill is a particular kind of [shim](#shim).

## Pure function

A function that has no side effects (does not modify external resources), and its output is only determined by the arguments. You could call this function 1M times, and given the same set of arguments, the output will always be the same.

## Reassignment

JavaScript with `var` and `let` declaration allows you to reassign a variable indefinitely. With `const` declarations you effectively declare an [immutable](#immutability) value for strings, integers, booleans, and an object that cannot be reassigned (but you can still modify it through its methods).

## Scope

Scope is the set of variables that's visible to a part of the program.

## Scoping

Scoping is the set of rules that's defined in a programming language to determine the value of a variable.

## Shim

A shim is a little wrapper around a functionality, or API. It's generally used to abstract something, pre-fill parameters or add a [polyfill](#polyfill) for browsers that do not support some functionality. You can consider it like a compatibility layer.

## Side effect

A side effect is when a function interacts with some other function or object outside it. Interaction with the network or the file system, or with the UI, are all side effects.

## State

State usually comes into play when talking about Components. A component can be stateful if it manages its own data, or stateless if it doesn't.

## Stateful

A stateful component, function or class manages its own state (data). It could store an array, a counter or anything else.

## Stateless

A stateless component, function or class is also called _dumb_ because it's incapable of having its own data to make decisions, so its output or presentation is entirely based on its arguments. This implies that [pure functions](#pure-function) are stateless. Note: in React, what we once called stateless components are now called function components because hooks give them the ability to use state.

## Strict mode

Strict mode is an ECMAScript 5.1 new feature, which causes the JavaScript runtime to catch more errors, but it helps you improve the JavaScript code by denying undeclared variables and other things that might cause overlooked issues like duplicated object properties and other subtle things. Hint: use it. The alternative is "sloppy mode" which is not a good thing even looking at the name we gave it.

## Tree Shaking

Tree shaking means removing "dead code" from the bundle you ship to your users. If you add some code that you never use in your import statements, that's not going to be sent to the users of your app, to reduce file size and loading time.