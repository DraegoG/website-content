---
title: "JavaScript Reference: String"
description: "All about the JavaScript String properties and methods"
date: 2019-03-13T07:00:00+02:00
tags: js
---

The String object has one static method, `String.fromCharCode()`, which is used to create a string representation from a sequence of Unicode characters. Here we build a simple string using the ASCII codes

```js
String.fromCodePoint(70, 108, 97, 118, 105, 111) //'Flavio'
```

You can also use octal or hexadecimal numbers:

```js
String.fromCodePoint(0x46, 0154, parseInt(141, 8), 118, 105, 111) //'Flavio'
```

All the other methods described here are **instance methods**: methods that are run on a string type.

## Instance methods

A string offers a few unique methods you can use:

- [`charAt(i)`](/javascript-string-charat/)
- [`charCodeAt(i)`](/javascript-string-charcodeat/)
- [`codePointAt(i)`](/javascript-string-codepointat/)
- [`concat(str)`](/javascript-string-concat/)
- [`endsWith(str)`](/javascript-string-endswith/)
- [`includes(str)`](/javascript-string-includes/)
- [`indexOf(str)`](/javascript-string-indexof/)
- [`lastIndexOf(str)`](/javascript-string-lastindexof/)
- [`localeCompare()`](/javascript-string-localecompare/)
- [`match(regex)`](/javascript-string-match/)
- [`normalize()`](/javascript-string-normalize/)
- [`padEnd()`](/javascript-string-padend/)
- [`padStart()`](/javascript-string-padstart/)
- [`repeat()`](/javascript-string-repeat/)
- [`replace(str1, str2)`](/javascript-string-replace/)
- [`search(str)`](/javascript-string-search/)
- [`slice(begin, end)`](/javascript-string-slice/)
- [`split(separator)`](/javascript-string-split/)
- [`startsWith(str)`](/javascript-string-startswith/)
- [`substring()`](/javascript-string-substring/)
- [`toLocaleLowerCase()`](/javascript-string-tolocalelowercase/)
- [`toLocaleUpperCase()`](/javascript-string-tolocaleuppercase/)
- [`toLowerCase()`](/javascript-string-tolowercase/)
- [`toString()`](/javascript-string-tostring/)
- [`toUpperCase()`](/javascript-string-touppercase/)
- [`trim()`](/javascript-string-trim/)
- [`trimEnd()`](/javascript-string-trimend/)
- [`trimStart()`](/javascript-string-trimstart/)
- [`valueOf()`](/javascript-string-valueof/)