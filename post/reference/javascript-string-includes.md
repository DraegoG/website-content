---
title: "The String includes() method"
description: "Find out all about the JavaScript includes() method of a string"
date: 2019-02-19T07:00:00+02:00
tags: js
---

Check if a string includes the value of the string `str`.

```js
'JavaScript'.includes('Script') //true
'JavaScript'.includes('script') //false
'JavaScript'.includes('JavaScript') //true
'JavaScript'.includes('aSc') //true
'JavaScript'.includes('C++') //false
```

`includes()` also accepts an optional second parameter, an integer which indicates the position where to start searching for:

```js
'a nice string'.includes('nice') //true
'a nice string'.includes('nice', 3) //false
'a nice string'.includes('nice', 2) //true
```