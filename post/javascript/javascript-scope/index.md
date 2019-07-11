---
title: JavaScript Scope
date: 2019-05-24T07:00:00+02:00
description: "Learn the basics of JavaScript Scope"
tags: js
---

Scoping is the set of rules that's defined in a programming language to determine the value of a variable.

JavaScript uses **lexical scoping**, which means that the value of a variable is defined by its position when it's written. Not when it's called, which is something that happens with the alternative, _dynamic scoping_.

Scope is the set of variables that's visible to a part of the program.

We have a global scope, block scope and function scope. If a variable is defined outside of a function or block, it's attached to the global object and it has a global scope, which mean it's available in every part of a program.

There is a very important difference between `var`, `let` and `const` declarations.

A variable defined as `var` inside a function is only visible inside that function. Just like function parameters.

A variable defined as `const` or `let` on the other hand is only visible inside that block where it resides.

It's important to understand that a block (identified by a pair of curly braces) does not define a new scope for `var`, but it does for `let` and `const`. A new scope for `var` is only created when a function is created, because `var` does not have block scope, but function scope.

Inside a function, any `var` variable defined in it is visible throughout all the function code, even if the variable is declared at the end of the function it can still be referenced in the beginning, because JavaScript before executing the code actually _moves all variable declarations on top_ (something that is called **hoisting**). To avoid confusion, always declare `var` variables at the beginning of a function.

This is what I mean. Even if you declare a `var` variable at the end of a function, its declaration is moved to the top:

```js
function run() {
  console.log(`${name}`)
  var name = 'Flavio'
}

run()
```

This prints "undefined", because what actually happens is:

```js
function run() {
  var name;
  console.log(`${name}`)
  name = 'Flavio'
}

run()
```

`let` and `const` do not "suffer" from hoisting. If you use one of them in the above example, you'd get an error: `ReferenceError: name is not defined`.

In JavaScript, variables of a parent function are made available to inner functions as well. The scope of an inner function also includes the scope of a parent function, and this is called closure (we'll talk more extensively about this later).

> There is one little thing you need to be aware of. In non-strict mode, if you use a variable without declaring it, wherever you do that, that variable is going to be attached to the global scope. Which can be a bad source of bugs. So, make sure you always declare variables before using them. Just be aware of this, but it's just another reason to use strict mode by default, which solves this issue. We'll talk about strict mode later.

Remember: any variable defined in a function (or block) with the same name as a global variable takes precedence over the global variable, shadowing it.

This prints `undefined`:

```js
var name = 'Roger'

function run() {
  console.log(`${name}`)
  var name = 'Flavio'
}

run()
```

and this raises an error `ReferenceError: name is not defined`:

```js
let name = 'Roger'

function run() {
  console.log(`${name}`)
  let name = 'Flavio'
}

run()
```
