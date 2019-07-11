---
title: "The String toLocaleUpperCase() method"
description: "Find out all about the JavaScript toLocaleUpperCase() method of a string"
date: 2019-03-05T07:00:00+02:00
tags: js
---

Returns a new string with the uppercase transformation of the original string, according to the locale case mappings.

The first parameter represents the locale, but it's optional (and if omitted, the current locale is used):

```js
'Testing'.toLocaleUpperCase() //'TESTING'
'Testing'.toLocaleUpperCase('it') //'TESTING'
'Testing'.toLocaleUpperCase('tr') //'TESTİNG'
```

Similar to the [`toUpperCase()`](/javascript-string-touppercase/) method, except that does not take locales into consideration.
