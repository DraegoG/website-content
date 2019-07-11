---
title: Introduction to the JavaScript Programming Language
date: 2018-01-26T16:04:59+02:00
description: "JavaScript is one of the most popular programming languages in the world, and now widely used also outside of the browser. The rise of Node.js in the last few years unlocked backend development, once the domain of Java, Ruby, Python, PHP, and more traditional server-side languages. Learn all about it!"
tags: js
tags_weight: 1
---

<!-- TOC -->

- [Introduction](#introduction)
- [A basic definition of JavaScript](#a-basic-definition-of-javascript)
- [JavaScript versions](#javascript-versions)

<!-- /TOC -->

## Introduction

JavaScript is one of the most popular programming languages in the world.

Created 20 years ago, it's gone a very long way since its humble beginnings.

Being the first - and the only - scripting language that was supported natively by web browsers, it just stuck.

In the beginnings, it was not nearly powerful as it is today, and it was mainly used for fancy animations and the marvel known at the time as DHTML.

With the growing needs that the web platform demands, JavaScript _had_ the responsibility to grow as well, to accommodate the needs of one of the most widely used ecosystems of the world.

Many things were introduced in the platform, with browser APIs, but the language grew quite a lot as well.

JavaScript is now widely used also outside of the browser. The rise of [Node.js](/nodejs/) in the last few years unlocked backend development, once the domain of Java, Ruby, Python and PHP and more traditional server-side languages.

JavaScript is now also the language powering databases and many more applications, and it's even possible to develop embedded applications, mobile apps, TV sets apps and much more. What started as a tiny language inside the browser is now the most popular language in the world.

## A basic definition of JavaScript

JavaScript is a programming language that is:

- **high level**: it provides abstractions that allow you to ignore the details of the machine where it's running on. It manages memory automatically with a garbage collector, so you can focus on the code instead of managing memory locations, and provides many constructs which allow you to deal with highly powerful variables and objects.
- **dynamic**: opposed to static programming languages, a dynamic language executes at runtime many of the things that a static language does at compile time. This has pros and cons, and it gives us powerful features like dynamic typing, late binding, reflection, functional programming, object runtime alteration, [closures](/javascript-closures/) and much more.
- **dynamically typed**: a variable does not enforce a type. You can reassign any type to a variable, for example assigning an integer to a variable that holds a string.
- **weakly typed**: as opposed to strong typing, weakly (or loosely) typed languages do not enforce the type of an object, allowing more flexibility but denying us type safety and type checking (something that [TypeScript](/typescript/) and Flow aim to improve)
- **interpreted**: it's commonly known as an interpreted language, which means that it does not need a compilation stage before a program can run, as opposed to C, Java or Go for example. In practice, browsers do compile JavaScript before executing it, for performance reasons, but this is transparent to you: there is no additional step involved.
- **multi-paradigm**: the language does not enforce any particular programming paradigm, unlike Java for example which forces the use of object oriented programming, or C that forces imperative programming. You can write JavaScript using an object-oriented paradigm, using prototypes and the new (as of ES6) classes syntax. You can write JavaScript in functional programming style, with its first class functions, or even in an imperative style (C-like).

In case you're wondering, _JavaScript has nothing to do with Java_, it's a poor name choice but we have to live with it.

## JavaScript versions

Let me introduce the term _ECMAScript_ here. We have a complete guide dedicated to [ECMAScript](/ecmascript/) where you can dive into it more, but to start with, you just need to know that ECMAScript (also called **ES**) is the name of the JavaScript standard.

JavaScript is an implementation of that standard. That's why you'll hear about [ES6, ES2015](/es6/), [ES2016](/es2016/), [ES2017](/es2017/), [ES2018](/es2018/) and so on.

For a very long time, the version of JavaScript that all browsers ran was ECMAScript 3. Version 4 was canceled due to feature creep (they were trying to add too many things at once), while ES5 was a huge version for JS.

[ES2015, also called ES6](/es6/), was huge as well.

Since then, the ones in charge decided to release one version per year, to avoid having too much time idle between releases, and have a faster feedback loop.

Currently, the latest approved JavaScript version is [ES2017](/es2017/).
