---
title: JavaScript Operators Precedence Rules
date: 2019-05-13T07:00:00+02:00
description: "Learn the basics of the JavaScript Operators Precedence Rules"
tags: js
---

Every complex statement will introduce precedence problems.

Take this:

```js
const a = 1 * 2 + 5 / 2 % 2
```

The result is 2.5, but why? What operations are executed first, and which need to wait?

Some operations have more precedence than the others. The precedence rules are listed in this table:

Operator | Description
---------|-------
`-` `+` `++` `--`  | unary operators, increment and decrement
`*` `/` `%` | multiply/divide
`+` `-` | addition/subtraction
`=` `+=` `-=` `*=` `/=` `%=` `**=` | assignments

Operations on the same level (like `+` and `-`) are executed in the order they are found

Following this table, we can solve this calculation:

```js
const a = 1 * 2 + 5 / 2 % 2
const a = 2 + 5 / 2 % 2
const a = 2 + 2.5 % 2
const a = 2 + 0.5
const a = 2.5
```
