---
title: "Introduction to CommonJS"
seotitle: "CommonJS JavaScript Module Format, an introduction"
date: 2018-06-14T07:06:15+02:00
updated: 2018-09-01T07:06:15+02:00
description: "The CommonJS module specification is the standard used in Node.js for working with modules. Modules are very cool, because they let you encapsulate all sorts of functionality, and expose this functionality to other JavaScript files, as libraries"
booktitle: CommonJS
tags: js
tags_weight: 38
---

The CommonJS module specification is the standard used in [Node.js](/nodejs/) for working with modules.

> Client-side JavaScript that runs in the browser uses another standard, called **ES Modules**

Modules are very cool, because they let you encapsulate all sorts of functionality, and expose this functionality to other JavaScript files, as libraries. They let you create clearly separate and reusable snippets of functionality, each testable on its own.

The huge [npm](/npm/) ecosystem is built upon this CommonJS format.

The syntax to import a module is:

```js
const package = require('module-name')
```

In CommonJS, modules are loaded synchronously, and processed in the order the JavaScript runtime finds them. This system was born with server-side JavaScript in mind, and is not suitable for the client-side (this is why ES Modules were introduced).

A JavaScript file is a module when it exports one or more of the symbols it defines, being them variables, functions, objects:

> uppercase.js

```js
exports.uppercase = str => str.toUpperCase()
```

Any JavaScript file can import and use this module:

```js
const uppercaseModule = require('uppercase.js')
uppercaseModule.uppercase('test')
```

A simple example can be found [in this Glitch](https://glitch.com/edit/#!/flavio-commonjs-example?path=server.js).

You can export more than one value:

```js
exports.a = 1
exports.b = 2
exports.c = 3
```

and import them individually using the [destructuring assignment](/es6/#destructuring-assignments):

```js
const { a, b, c } = require('./uppercase.js')
```

or just export one value using:

```js
//file.js
module.exports = value
```

and import it using

```js
const value = require('./file.js')
```