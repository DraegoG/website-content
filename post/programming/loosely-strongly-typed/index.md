---
title: Loosely typed vs strongly typed languages
date: 2019-01-20T07:00:00+02:00
description: "The key differences between using a loosely typed language compared to a strongly typed languages"
tags: js
---

In programming we call a language **loosely typed** when you don't have to explicitly specify types of variables and objects.

A **strongly typed** language on the contrary wants types specified.

There are pros and cons, you can argue forever but the reality is that both approaches are great, in their intended context and usage.

JavaScript is loosely typed. You don't have to tell that a string is a string, nor you can require a function to accepts an integer as its parameter.

This gives JavaScript a lot of flexibility. Flexibility lets you move faster, change things quickly, iterate at a faster velocity.

A strong type system instead gives much more structure to a program and it's a great aid for example when working in teams, when one single programmer can't really have all the codebase in mind when working on it, and having types helps keep the code manageable.

This is typical of compiled languages (while famous dynamic languages like JavaScript, Python and Ruby are loosely typed).

You trade some of the flexibility that a loosely typed language gives you to get more security and trust in the codebase.

The compiler thanks to types can detect errors at compile time, rather than at runtime, making it simpler to write code that does what you want (and makes the testing phase slightly easier, although nothing can make your programs perfect).

[TypeScript](/typescript/) is a great example of a strongly typed language. It compiles to JavaScript, giving you the benefit of the JavaScript platform plus the intended advantages of types. C, Go, Java and Swift are great examples of strongly typed languages.

Being loosely typed doesn't mean you don't have types, of course, as you can see in my [JavaScript Types](/javascript-types/) post. You just make use of types implicitly, with the pros and cons that you imagine.