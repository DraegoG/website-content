---
title: "The String padStart() method"
description: "Find out all about the JavaScript padStart() method of a string"
date: 2019-02-26T07:00:00+02:00
tags: js
---

The purpose of string padding is to **add characters to a string**, so it **reaches a specific length**.

`padStart()` can be used to add characters at the beginning of a string.

```js
padStart(targetLength [, padString])
```

Sample usage:

| padStart()                  |              |
| --------------------------- |:-------------|
| 'test'.padStart(4)          | 'test'       |
| 'test'.padStart(5)          | '&nbsp;test'      |
| 'test'.padStart(8)          | '&nbsp;&nbsp;&nbsp;&nbsp;test'   |
| 'test'.padStart(8, 'abcd')  | 'abcdtest'   |


Also see [`padEnd()`](/javascript-string-padend/).