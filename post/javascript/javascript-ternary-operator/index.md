---
title: JavaScript Ternary Operator
date: 2019-06-15T07:00:00+02:00
description: "Learn the basics of the JavaScript Ternary Operator"
tags: js
---

The **ternary operator** is the only operator in JavaScript that works with 3 operands, and it's a short way to express conditionals.

This is how it looks:

```js
<condition> ? <expression> : <expression>
```

The condition `<condition>` is evaluated as a boolean, and upon the result, the operator runs the first expression (if the condition is true) or the second.

This is an example: we check if `running` equals to true, and if this is the case we call the `stop()` function. Otherwise we call the `run()` function:

Example usage:

```js
const running = true;
(running === true) ? stop() : run()
```
