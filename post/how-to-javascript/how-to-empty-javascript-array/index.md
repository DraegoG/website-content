---
title: How to empty a JavaScript array
description: "Given a JavaScript array, see how to clear it and empty all its elements"
date: 2018-12-03T07:00:00+02:00
tags: js
---

There are various ways to empty a JavaScript array.

The easiest one is to set its length to 0:

```js
const list = ['a', 'b', 'c']
list.length = 0
```

Another method mutates the original array reference, assigning an empty array to the original variable, so it requires using `let` instead of `const`:

```js
let list = ['a', 'b', 'c']
list = []
```

