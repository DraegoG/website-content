---
title: JavaScript Assignment Operator
date: 2019-04-28T07:00:00+02:00
description: "Learn the basics of the JavaScript Assignment Operator"
tags: js
---

Use the assignment operator `=` to assign a value to a variable:

```js
const a = 2
let b = 2
var c = 2
```

This operator has several shortcuts for all the arithmetic operators which let you assign to the first operand the result of the operations with the second operand.

They are:

- `+=`: addition assignment
- `-=`: subtraction assignment
- `*=`: multiplication assignment
- `/=`: division assignment
- `%=`: remainder assignment
- `**=`: exponentiation assignment

Examples:

```js
let a = 0
a += 5 //a === 5
a -= 2 //a === 3
a *= 2 //a === 6
a /= 2 //a === 3
a %= 2 //a === 1
```

> To be clear, the above operations are executed one after another, so `a` at the end is 1, not 0