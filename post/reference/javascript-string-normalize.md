---
title: "The String normalize() method"
description: "Find out all about the JavaScript normalize() method of a string"
date: 2019-02-24T07:00:00+02:00
tags: js
---

Unicode has four main *normalization forms*. Their codes are `NFC`, `NFD`, `NFKC`, `NFKD`. [Wikipedia has a good explanation of the topic](https://en.wikipedia.org/wiki/Unicode_equivalence).

The `normalize()` method returns the string normalized according to the form you specify, which you pass as parameter (`NFC` being the default if the parameter is not set).

I will reuse the MDN example because I'm sure there is a valid usage but I can't find another example:

```js
'\u1E9B\u0323'.normalize() //ẛ̣
'\u1E9B\u0323'.normalize('NFD') //ẛ̣
'\u1E9B\u0323'.normalize('NFKD') //ṩ
'\u1E9B\u0323'.normalize('NFKC') //ṩ
```