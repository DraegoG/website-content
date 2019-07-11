---
title: JavaScript Recursion
date: 2019-06-17T07:00:00+02:00
description: "Learn the basics of Recursion in JavaScript"
tags: js
---

**A function can call itself**.

This is what recursion means. And it allows us to solve problems in a neat way.

To do so, you need a named function expression, in other words this:

```js
function doSomething() {

}
```

So we can call `doSomething()` inside `doSomething()`.

The simplest example we can make is calculating a factorial of a number. This is the number that we get by multiplying the number for (number - 1), (number - 2), and so on until we reach the number 1.

The factorial of 4 is (4 * (4 - 1) * (4 - 2) * (4 - 3)) = 4 * 3 * 2 * 1, which is 24.

We can create a recursive function to calculate it automatically:

```js
function factorial(n) {
  return n >= 1 ? n * factorial(n - 1) : 1
}

factorial(1) //1
factorial(2) //2
factorial(3) //6
factorial(4) //24
```

We can also use an arrow function if we prefer:

```js
const factorial = (n) => {
  return n >= 1 ? n * factorial(n - 1) : 1
}

factorial(1) //1
factorial(2) //2
factorial(3) //6
factorial(4) //24
```

Now it's a good time to talk about the **call stack**.

Imagine we do an error, and instead of calculating the factorial as

```js
const factorial = (n) => {
  return n >= 1 ? n * factorial(n - 1) : 1
}
```

we do this:

```js
const factorial = (n) => {
  return n >= 1 ? n * factorial(n) : 1
}
```

As you can see, we are calling `factorial(n)` ad infinitum. There's no end, because we forgot to lower it on every call.

If you run this code, you'll get this error:

```
RangeError: Maximum call stack size exceeded
```

Every time a function is invoked, JavaScript needs to remember the current context before switching to the new one, so it puts that context on the **call stack**. As soon as the function returns, JavaScript goes to the call stack and picks the last element that was added, and resumes its execution.

Maximum call stack size exceeded means that too many elements were put on the stack, and your program crashed.
