---
title: "The String charCodeAt() method"
description: "Find out all about the JavaScript charCodeAt() method of a string"
date: 2019-02-15T07:00:00+02:00
tags: js
---

Return the character code at the index `i`. Similar to `charAt()`, except it returns the Unicode 16-bit integer representing the character:

```js
'Flavio'.charCodeAt(0) //70
'Flavio'.charCodeAt(1) //108
'Flavio'.charCodeAt(2) //97
```

Calling `toString()` after that will return the hexadecimal number, which you can lookup in Unicode tables like [this](https://apps.timwhitlock.info/emoji/tables/unicode).