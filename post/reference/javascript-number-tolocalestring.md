---
title: "The Number toLocaleString() method"
description: "Find out all about the JavaScript toLocaleString() method of a number"
date: 2019-03-23T07:00:00+02:00
tags: js
---

Formats a number according to a locale.

By default the locale is US english:

```js
new Number(21.2).toLocaleString() //21.2
```

We can pass the locale as the first parameter:

```js
new Number(21.2).toLocaleString('it') //21,2
```

This is eastern arabic

```js
new Number(21.2).toLocaleString('ar-EG') //٢١٫٢
```

There are a number of options you can add, and I suggest to look at the [MDN page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString) to know more.
