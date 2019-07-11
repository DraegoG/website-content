---
title: "Things to avoid in JavaScript (the bad parts)"
description: "A quick list of things to avoid when writing JavaScript code"
date: 2012-07-16T09:03:46+02:00
tags: js
tags_weight: 47
---

- Avoid creating a new object by using `new Object()`. Use the object literal syntax `{}` instead.
- Same thing for arrays, favor `[]` over `new Array()`.
- Avoid blocks except where statements require them (`if`, `switch`, loops, `try`).
- Never assign inside an `if` of `while` statements condition part
- Never use `==` and `!=`. Use `===` and `!==` instead.
- Never use `eval`. Why? It has performance issues (it runs the interpreter/compiler), it has security issues (code injection if used with user input), difficulties in debugging.
- Never use `with`, as it modifies the scope chain and can be a source of confusion.
- Always pass functions to [`setTimeout` and `setInterval`](/javascript-timers/)
- Never use `Array` as an associative arrays, use `Object` instead. The part of the `Array` object that provides that functionality is in fact provided by the `Object` prototype, so you could really have used a `Date` object for that same thing.
- Don't use `\` at the end of a string to create a multiline string, it's not part of ECMAScript. Use string concatenation `' string1 ' + ' string2 '` instead
- Never modify the prototypes of the built-in objects `Object` and `Array`. Modify other prototypes of other objects such as `Function` with caution as it could lead to bugs hard to debug.

