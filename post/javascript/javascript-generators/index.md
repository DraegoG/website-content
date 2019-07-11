---
title: "JavaScript Generators Tutorial"
description: "Generators are a special kind of function with the ability to pause itself, and resume later, allowing other code to run in the meantime."
date: 2019-01-29T07:00:00+02:00
tags: js
---

Generators are a special kind of function with the ability to pause itself, and resume later, allowing other code to run in the meantime.

See the full JavaScript Generators Guide for a detailed explanation of the topic.

The code decides that it has to wait, so it lets other code "in the queue" to run, and keeps the right to resume its operations "when the thing it's waiting for" is done.

All this is done with a single, simple keyword: `yield`. When a generator contains that keyword, the execution is halted.

A generator can contain many `yield` keywords, thus halting itself multiple times, and it's identified by the `*function` keyword, which is not to be confused with the pointer dereference operator used in lower level programming languages such as C, C++ or Go.

Generators enable whole new paradigms of programming in JavaScript, allowing:

- 2-way communication while a generator is running
- long-lived while [loops](/javascript-loops/) which do not freeze your program

Here is an example of a generator which explains how it all works.

```js
function *calculator(input) {
    var doubleThat = 2 * (yield (input / 2))
    var another = yield (doubleThat)
    return (input * doubleThat * another)
}
```

We initialize it with

```js
const calc = calculator(10)
```

Then we start the iterator on our generator:

```js
calc.next()
```

This first iteration starts the iterator. The code returns this object:

```js
{
  done: false
  value: 5
}
```

What happens is: the code runs the function, with `input = 10` as it was passed in the generator constructor. It runs until it reaches the `yield`, and returns the content of `yield`: `input / 2 = 5`. So we got a value of 5, and the indication that the iteration is not done (the function is just paused).

In the second iteration we pass the value `7`:

```js
calc.next(7)
```

and what we got back is:

```js
{
  done: false
  value: 14
}
```

`7` was placed as the value of `doubleThat`. Important: you might read like `input / 2` was the argument, but that's just the return value of the first iteration. We now skip that, and use the new input value, `7`, and multiply it by 2.

We then reach the second yield, and that returns `doubleThat`, so the returned value is `14`.

In the next, and last, iteration, we pass in 100

```js
calc.next(100)
```

and in return we got

```js
{
  done: true
  value: 14000
}
```

As the iteration is done (no more yield keywords found) and we just return `(input * doubleThat * another)` which amounts to `10 * 14 * 100`.
