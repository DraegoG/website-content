---
title: "The String toLocaleLowerCase() method"
description: "Find out all about the JavaScript toLocaleLowerCase() method of a string"
date: 2019-03-04T07:00:00+02:00
tags: js
---

Returns a new string with the lowercase transformation of the original string, according to the locale case mappings.

The first parameter represents the locale, but it's optional (and if omitted, the current locale is used):

```js
'Testing'.toLocaleLowerCase() //'testing'
'Testing'.toLocaleLowerCase('it') //'testing'
'Testing'.toLocaleLowerCase('tr') //'testing'
```

As usual with internationalization we might not recognize the benefits, but I read on MDN that Turkish does not have the same case mappings at other languages, to start with.

Similar to the [`toLowerCase()`](/javascript-string-tolowercase/) method, except that does not take locales into consideration.
