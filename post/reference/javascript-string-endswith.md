---
title: "The String endsWith() method"
description: "Find out all about the JavaScript endsWith() method of a string"
date: 2019-02-18T07:00:00+02:00
tags: js
---

Check if a string ends with the value of the string `str`.

```js
'JavaScript'.endsWith('Script') //true
'JavaScript'.endsWith('script') //false
```

You can pass a second parameter with an integer value and (if present) `endsWith()` will consider the original string as if it was long that many characters:

```js
'JavaScript'.endsWith('Script', 5) //false
'JavaScript'.endsWith('aS', 5) //true
```

It was introduced in [ECMAScript 2015](/es6/).