---
title: "JavaScript Exceptions"
description: "When the code runs into an unexpected problem, the JavaScript idiomatic way to handle this situation is through exceptions"
date: 2018-07-25T07:06:29+02:00
booktitle: Exceptions
tags: js
tags_weight: 9
---

When the code runs into an unexpected problem, the JavaScript idiomatic way to handle this situation is through exceptions.

## Creating exceptions

An exception is created using the `throw` keyword:

```js
throw value
```

where `value` can be any JavaScript value including a string, a number or an object.

As soon as JavaScript executes this line, the normal program flow is halted and the control is held back to the nearest **exception handler**.

## Handling exceptions

An exception handler is a `try`/`catch` statement.

Any exception raised in the lines of code included in the `try` block is handled in the corresponding `catch` block:

```js
try {
  //lines of code
} catch (e) {

}
```

`e` in this example is the exception value.

You can add multiple handlers, that can catch different kinds of errors.

## `finally`

To complete this statement JavaScript has another statement called `finally`, which contains code that is executed regardless of the program flow, if the exception was handled or not, if there was an exception or if there wasn't:

```js
try {
  //lines of code
} catch (e) {

} finally {

}
```

You can use `finally` without a `catch` block, to serve as a way to clean up any resource you might have opened in the `try` block, like files or network requests:

```js
try {
  //lines of code
} finally {

}
```

## Nested `try` blocks

`try` blocks can be nested, and an exception is always handled in the nearest catch block:

```js
try {
  //lines of code

  try {
    //other lines of code
  } finally {
    //other lines of code
  }

} catch (e) {

}
```

If an exception is raised in the inner `try`, it's handled in the outer `catch` block.