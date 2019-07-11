---
title: How to create a multiline string in JavaScript
description: "Discover how to create a multiline string"
date: 2018-09-30T07:00:00+02:00
tags: js
---

JavaScript never had a true good way to handle multiline strings, until 2015 when ES6 was introduced, along with [template literals](/javascript-template-literals/).


Template literals are strings delimited by backticks, instead of the normal single/double quote delimiter.

They have a unique feature: they allow multiline strings:

```js
const multilineString = `A string
on multiple lines`

const anotherMultilineString = `Hey
this is cool
a multiline
st
r
i
n
g
!
`
```
