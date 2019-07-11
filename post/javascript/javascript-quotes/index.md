---
title: Quotes in JavaScript
description: "An overview of the quotes allowed in JavaScript and their unique features"
date: 2018-08-02T07:07:09+02:00
booktitle: Quotes
tags: js
tags_weight: 11
---

JavaScript allows you to use 3 types of quotes:

- single quotes
- double quotes
- backticks

The first 2 are essentially the same:

```js
const test = 'test'
const bike = "bike"
```

There's little to no difference in using one or the other. The only difference lies in having to escape the quote character you use to delimit the string:

```js
const test = 'test'
const test = 'te\'st'
const test = 'te"st'
const test = "te\"st"
const test = "te'st"
```

There are various style guides that recommend always using one style vs the other.

I personally prefer single quotes all the time, and use double quotes only in HTML.

Backticks are a recent addition to JavaScript, since they were introduced with ES6 in 2015.

They have a unique feature: they allow multiline strings.

Multiline strings are also possible using regular strings, using escape characters:

```js
const multilineString = 'A string\non multiple lines'
```

Using backticks, you can avoid using an escape character:

```js
const multilineString = `A string
on multiple lines`
```

Not just that. You can interpolate variables using the `${}` syntax:

```js
const multilineString = `A string
on ${1+1} lines`
```

[I cover backticks-powered strings (called template literals) in a separate article](/javascript-template-literals/), that dives more into the nitty-gritty details.