---
title: "How to trim the leading zero in a number in JavaScript"
date: 2018-07-05T07:06:15+02:00
description: "If you have a number with a leading zero, like 010 or 02, how to remove that zero?"
tags: js
---

If you have a number with a leading zero, like `010` or `02`, how to remove that zero?

There are various ways.

The most explicit is to use `parseInt()`:

```js
parseInt(number, 10)
```

10 is the radix, and should be always specified to avoid inconsistencies across different browsers, although some engines work fine without it.

Another way is to use the `+` unary operator:

```js
+number
```

Those are the simplest solutions.

You can also go the [regular expression](/javascript-regular-expressions/) route, like this:

```js
number.replace(/^0+/, '')
```
