---
title: JavaScript Private Class Fields
date: 2019-07-09T07:00:00+02:00
description: "Introduction and code samples on using private class fields in JavaScript."
tags: js
---

Before the introduction of private class fields, we could not really enforce private properties on a class. We used conventions instead, maybe using `_` as an hint that the field is private, like this:

```js
class Counter {
  _count = 0

  increment() {
    this._count++
  }
}
```

But we could access the count using

```js
const counter = new Counter()
counter._count
```

We can now use private class fields that enforce private fields:

```js
class Counter {
  #count = 0

  increment() {
    this.#count++
  }
}
```

We now can't access this value from the outside. Trying to access it will raise a syntax error.

This is part of the new [class fields proposal](https://github.com/tc39/proposal-class-fields), which you can use since Chrome 72 and Node 12.