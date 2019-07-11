---
title: JavaScript Loops and Scope
date: 2018-03-01T09:07:09+02:00
description: "There is one feature of JavaScript that might cause a few headaches to developers, related to loops and scoping. Learn some tricks about loops and scoping with var and let"
booktitle: Loops and Scope
tags: js
tags_weight: 24
---

There is one feature of [JavaScript](/javascript/) that might cause a few headaches to developers, related to loops and scoping.

Take this example:

```js
const operations = []

for (var i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

It basically iterates and for 5 times it adds a function to an array called operations. This function console logs the loop index variable `i`.

Later it runs these functions.

The expected result here should be:

```
0
1
2
3
4
```

but actually what happens is this:

```
5
5
5
5
5
```

Why is this the case? Because of the use of `var`.

Since `var` declarations are **hoisted**, the above code equals to

```js
var i;
const operations = []

for (i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

so, in the for-of loop, `i` is still visible, it's equal to 5 and every reference to `i` in the function is going to use this value.

So how should we do to make things work as we want?

The simplest solution is to use `let` declarations. Introduced in ES6, they are a great help in avoiding some of the weird things about `var` declarations.

Changing `var` to `let` in the loop variable is going to work fine:

```js
const operations = []

for (let i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
  })
}

for (const operation of operations) {
  operation()
}
```

Here's the output:

```
0
1
2
3
4
```

How is this possible? This works because on every loop iteration `i` is created as a new variable each time, and every function added to the `operations` array gets its own copy of `i`.

Keep in mind you cannot use `const` in this case, because there would be an error as `for` tries to assign a new value in the second iteration.

Another way to solve this problem was very common in pre-ES6 code, and it is called **Immediately Invoked Function Expression** (IIFE).

In this case you can wrap the entire function and bind `i` to it. Since in this way you're creating a function that immediately executes, you return a new function from it, so we can execute it later:

```js
const operations = []

for (var i = 0; i < 5; i++) {
  operations.push(((j) => {
    return () => console.log(j)
  })(i))
}

for (const operation of operations) {
  operation()
}
```