---
title: The JavaScript if/else conditional
date: 2019-06-01T07:00:00+02:00
description: "Learn the basics of the JavaScript `if` conditional"
tags: js
---

An `if` statement is used to make the program take a route, or another, depending on the result of an expression evaluation.

This is the simplest example, which always executes:

```js
if (true) {
  //do something
}
```

on the contrary, this is never executed:

```js
if (false) {
  //do something (? never ?)
}
```

If you have a single statement to execute after the conditionals, you can omit the block, and just write the statement:

```js
if (true) doSomething()
```

The conditional checks the expression you pass to it for true or false value. If you pass a number, that always evaluates to true unless it's 0. If you pass a string, it always evaluates to true unless it's an empty string. Those are general rules of casting types to a boolean.

## Else

You can provide a second part to the `if` statement: `else`.

You attach a statement that is going to be executed if the `if` condition is false:

```js
if (true) {
  //do something
} else {
  //do something else
}
```

Since `else` accepts a statement, you can nest another if/else statement inside it:

```js
if (a === true) {
  //do something
} else if (b === true) {
  //do something else
} else {
  //fallback
}
```
