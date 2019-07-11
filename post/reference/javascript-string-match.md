---
title: "The String match() method"
description: "Find out all about the JavaScript match() method of a string"
date: 2019-02-23T07:00:00+02:00
tags: js
---

Given a regular expression identified by `regex`, try to match it in the string.

Examples:

```js
'Hi Flavio'.match(/avio/)
// Array [ 'avio' ]

'Test 123123329'.match(/\d+/)
// Array [ "123123329" ]

'hey'.match(/(hey|ho)/)
//Array [ "hey", "hey" ]

'123s'.match(/^(\d{3})(\w+)$/)
//Array [ "123s", "123", "s" ]

'123456789'.match(/(\d)+/)
//Array [ "123456789", "9" ]

'123s'.match(/^(\d{3})(?:\s)(\w+)$/)
//null

'123 s'.match(/^(\d{3})(?:\s)(\w+)$/)
//Array [ "123 s", "123", "s" ]

'I saw a bear'.match(/\bbear/)    //Array ["bear"]

'I saw a beard'.match(/\bbear/)   //Array ["bear"]

'I saw a beard'.match(/\bbear\b/) //null

'cool_bear'.match(/\bbear\b/)     //null
```

To know more about Regular Expressions, see my [Regular Expressions tutorial](/javascript-regular-expressions/).
