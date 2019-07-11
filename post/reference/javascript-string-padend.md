---
title: "The String padEnd() method"
description: "Find out all about the JavaScript padEnd() method of a string"
date: 2019-02-25T07:00:00+02:00
tags: js
---

The purpose of string padding is to **add characters to a string**, so it **reaches a specific length**.

`padEnd()`, introduced in ES2017, adds such characters at the end of the string.

```js
padEnd(targetLength [, padString])
```

Sample usage:

| padEnd()                  |              |
| ------------------------- |:-------------|
| 'test'.padEnd(4)          | 'test'       |
| 'test'.padEnd(5)          | 'test&nbsp;'      |
| 'test'.padEnd(8)          | 'test&nbsp;&nbsp;&nbsp;&nbsp;'   |
| 'test'.padEnd(8, 'abcd')  | 'testabcd'   |

Also see [`padStart()`](/javascript-string-padstart/).