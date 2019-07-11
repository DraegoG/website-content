---
title: JavaScript Closures explained
description: "A gentle introduction to the topic of closures, key to understanding how JavaScript functions work"
date: 2018-04-23T07:04:59+02:00
booktitle: "Closures"
tags: js
tags_weight: 14
---

If you've ever written a [function](/javascript-functions/) in JavaScript, you already made use of **closures**.

It's a key topic to understand, which has implications on the things you can do.

When a function is run, it's executed **with the scope that was in place when it was defined**, and _not_ with the state that's in place when it is **executed**.

The scope basically is the set of variables which are visible.

A function remembers its [Lexical Scope](/javascript-glossary/#lexical-scoping), and it's able to access variables that were defined in the parent scope.

In short, a function has an entire baggage of variables it can access.

Let me immediately give an example to clarify this.

```js
const bark = dog => {
  const say = `${dog} barked!`
  ;(() => console.log(say))()
}

bark(`Roger`)
```

This logs to the console `Roger barked!`, as expected.

What if you want to return the action instead:

```js
const prepareBark = dog => {
  const say = `${dog} barked!`
  return () => console.log(say)
}

const bark = prepareBark(`Roger`)

bark()
```

This snippet also logs to the console `Roger barked!`.

Let's make one last example, which reuses `prepareBark` for two different dogs:

```js
const prepareBark = dog => {
  const say = `${dog} barked!`
  return () => {
    console.log(say)
  }
}

const rogerBark = prepareBark(`Roger`)
const sydBark = prepareBark(`Syd`)

rogerBark()
sydBark()
```

This prints

```
Roger barked!
Syd barked!
```

As you can see, the **state** of the variable `say` is linked to the function that's returned from `prepareBark()`.

Also notice that we redefine a new `say` variable the second time we call `prepareBark()`, but that does not affect the state of the first `prepareBark()` scope.

This is how a closure works: the function that's returned keeps the original state in its scope.
