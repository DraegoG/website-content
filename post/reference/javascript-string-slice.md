---
title: "The String slice() method"
description: "Find out all about the JavaScript slice() method of a string"
date: 2019-02-28T07:00:00+02:00
tags: js
---

Return a new string from the part of the string included between the `begin` and `end` positions.

The original string is not mutated.

`end` is optional.

```js
'This is my car'.slice(5) //is my car
'This is my car'.slice(5, 10) //is my
```

If you set a negative first parameter, the start index starts from the end, and the second parameter must be negative as well, always counting from the end:

```js
'This is my car'.slice(-6) //my car
'This is my car'.slice(-6, -4) //my
```