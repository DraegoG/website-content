---
title: JavaScript Statements
date: 2019-05-21T07:00:00+02:00
description: "Learn the basics of JavaScript Statements"
tags: js
---

If expressions are single units of JavaScript that the engine can evaluate, statements can contain one or more different expressions, and are executed by the engine to perform an operation.

Programs are composed by multiple statements. Statements can span over multiple lines.

Just like with expressions, JavaScript has a whole different set of statements:

- expression statements
- declaration statements
- control flow statements
- loop statements
- miscellaneous statements

Let's dive into the details.

## Separating statements

Statements can end with an optional semicolon `;`. Using it, you can have multiple statements on a single line. I normally don't use semicolons, but you can use it whenever a statement ends.

## Expression statements

An expression on its own is also a statement:

```js
2
0.02
'something'
true
false
this //the current scope
undefined
i //where i is a variable or a constant
1 / 2
i++
i -= 2
i * 2
'A ' + 'string'
[] //array literal
{} //object literal
[1,2,3]
{a: 1, b: 2}
{a: {b: 1}}
a && b
a || b
!a
object.property //reference a property (or method) of an object
object[property]
object['property']
new object()
new a(1)
new MyRectangle('name', 2, {a: 4})
function() {}
function(a, b) { return a * b }
(a, b) => a * b
a => a * 2
() => { return 2 }
a.x(2)
window.resize()
```

## Declaration statements

With a declaration statement you assign a value to a variable name.

Examples:

```js
var i = 0
let j = 1
const k = 2

//declare an object value
const car = {
  color: blue
}
```

Here are function declarations:

```js
//declare a function
function fetchFromNetwork() {
  //...
}
//or
const fetchFromNetwork = () => {
  //...
}
```

## Control flow statements

Statements can be grouped, using a block:

```js
{
  //this is a block
  const a = 1;
  const b = 2;
}
```

Using this syntax, you can have multiple statements whenever JavaScript expects a single statement.

We'll talk about control flow very soon. But in the meantime just be aware that any of the conditional control flow statements check an expression and depending on it they execute a statement, or a block:

```js
if (condition === true) {
  //execute this block
} else {
  //execute this block
}
```

You can omit curly braces if you only have one statement:

```js
if (condition === true) /* statement */ else /* another statement */
```

I'll go into all the different control flow structures in the next sections.

## Loop statements

Loops is a big argument as well. We'll explore loops very soon, in the meantime just know that they work similarly to the `if` example above.

Some loops check an expression, and repeat a statement execution it until that  expression evaluates to true.

Some other loops iterate over a list and execute a statement (or block) for each element of the list, until the list finishes.

## Miscellaneous statements

### `return <expression>`

This statement returns a value from a function, ending the function execution.

### `throw <expression>`

Throws an exception (we'll later see what is an exception)

### `try` and `catch`

A try/catch block is used to catch exceptions. Again, we'll see those applied later on.

```js
try {

} catch (<expression>) {

}
```

### `use strict`

This statement applies strict mode (we'll soon see what that means)

### `debugger`

Adds a breakpoint which the debugger can use. We'll soon see it in practice.
