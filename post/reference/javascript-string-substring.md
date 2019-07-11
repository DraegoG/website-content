---
title: "The String substring() method"
description: "Find out all about the JavaScript substring() method of a string"
date: 2019-03-03T07:00:00+02:00
tags: js
---

`substring()` returns a portion of a string and it's similar to [`slice()`](/javascript-string-slice/), with some key differences.

If any parameter is negative, it is converted to `0`.
If any parameter is higher than the string length, it is converted to the length of the string.

So:

```js
'This is my car'.substring(5) //'is my car'
'This is my car'.substring(5, 10) //'is my'
'This is my car'.substring(5, 200) //'is my car'
'This is my car'.substring(-6) //'This is my car'
'This is my car'.substring(-6, 2) //'Th'
'This is my car'.substring(-6, 200) //'This is my car'
```
