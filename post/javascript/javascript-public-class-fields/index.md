---
title: JavaScript Public Class Fields
description: "A simple tutorial on the new JavaScript Public Class Fields"
date: 2019-07-23T07:00:00+02:00
tags: js
---

In the past, to create a public class field we would have used this syntax, instantiating the field in the constructor:

```js
class Counter {
  constructor() {
    this.count = 0
  }
}
```

The new [class fields proposal](https://github.com/tc39/proposal-class-fields), which you can use since Chrome 72 and Node 12, allows us to use this syntax:

```js
class Counter {
  count = 0
}
```

Much simpler!