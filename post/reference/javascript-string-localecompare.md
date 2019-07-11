---
title: "The String localeCompare() method"
description: "Find out all about the JavaScript localeCompare() method of a string"
date: 2019-02-22T07:00:00+02:00
tags: js
---

This method compares a string to another, returning a number (negative, 0, positive) that tells if the current string is lower, equal or greater than the string passed as argument, according to the locale.

The locale is determined by the current locale, or you can pass it as a second argument:

```js
'a'.localeCompare('à') //-1
'a'.localeCompare('à', 'it-IT') //-1
```

The most common use case is for ordering arrays:

```js
['a', 'b', 'c', 'd'].sort((a, b) => a.localeCompare(b))
```

where one would typically use

```js
['a', 'b', 'c', 'd'].sort((a, b) => (a > b) ? 1 : -1)
```

with the difference that `localeCompare()` allows us to make this compatible with alphabets used all over the globe.

An object passed as third argument can be used to pass additional options. Look for all the possible values of those options [on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare).