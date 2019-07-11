---
title: JavaScript Coding Style
description: This JavaScript Coding Style is the set of conventions I use every day when using JavaScript. It's a live document, with the main set of rules I follow
date: 2014-01-11T09:06:29+02:00
updated: 2019-04-27T13:06:29+02:00
tags: js
---

Every language has a set of rules when it comes to syntax.

When starting out, some people might add code into a file following without breaking the language rules, but without giving care and attention to the programming **style**.

Not because they don't care about style,they are not experienced enough to recognize its importance.

I really believe programming is a craft. Like painting, or wood crafting, or anything that involves creativity, our programs can do many things but they should do it in style.

We have some rules that are valid across all programming languages.

A coding style is an **agreement with yourself and your team**, to keep consistency on a project.

If you don't have a team, it's an **agreement with you**, to always keep your code up to your standards.

Having fixed rules on your code writing format helps a lot in order to have a **more readable and managed code**.

## Popular Style Guides

There are a quite a few of them around, here are the 2 most common ones in the [JavaScript](/javascript/) world:

- [The Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [The AirBnb JavaScript Style Guide](https://github.com/airbnb/javascript)

It's up to you to follow one of those, or create your own style guide.

## Be consistent with the project you work on

Even if you prefer a set of styles, when working on a project you should use that project style.

An Open Source project on GitHub might follow a set of rules, another project you work on with a team might follow an entirely different one.

[Prettier](/prettier/) is an awesome tool that enforces code formatting, use it.

## My own preferences

My own take on JavaScript style is:

Always use the latest ES version. Use Babel if old browser support is necessary.

**Indentation**: use spaces instead of tabs, indent using 2 spaces.

**Semicolons**: don't use semicolons.

**Line length**: try to cut lines at 80 chars, if possible.

**Inline Comments**: use inline comments in your code. Use block comments only to document.

**No dead code**: Don't leave old code commented, "just in case" it will be useful later. Keep only the code you need now, version control/your notes app is meant for this.

**Only comment when useful**: Don't add comments that don't help understand what the code is doing. If the code is self-explaining through the use of good variable and function naming, and JSDoc function comments, don't add a comment.

**Variable declarations**: always declare variables to avoid polluting the global object. Never use `var`. Default to `const`, only use `let` if you reassign the variable.

**Functions**: use arrow functions unless you have a specific reason to use regular functions, like in object methods or constructors, due to how `this` works. Declare them as const, and use implicit returns if possible.

```js
const test = (a, b) => a + b

const another = a => a + 2
```

Feel free to use nested functions to hide helper functions to the rest of the code.

**Names**: function names, variable names and method names always start with a lowercase letter (unless you identify them as private, read below), and are camelCased. Only constructor functions and class names should start capitalized. If you use a framework that requires specific conventions, change your habits accordingly. File names should all be lowercase, with words separated by `-`.

**Statement-specific formats and rules**:

**if**

```js
if (condition) {
  statements
}

if (condition) {
  statements
} else {
  statements
}

if (condition) {
  statements
} else if (condition) {
  statements
} else {
  statements
}
```

**for**

Always initialize the length in the initialization to cache it, don't insert it in the condition.

Avoid using `for in` except with used in conjunction with `.hasOwnProperty()`. Prefer `for of` (see [JavaScript Loops](/javascript-loops))

```js
for (initialization; condition; update) {
  statements
}
```

**while**

```js
while (condition) {
  statements
}
```

**do**

```js
do {
  statements
} while (condition);
```

**switch**

```js
switch (expression) {
  case expression:
    statements
  default:
    statements
}
```

**try**

```js
try {
  statements
} catch (variable) {
  statements
}

try {
  statements
} catch (variable) {
  statements
} finally {
  statements
}
```

**Whitespace**: use whitespace wisely to improve readability: put a whitespace after a keyword followed by a `(`; before & after a binary operation (`+`, `-`, `/`, `*`, `&&`..); inside the for statement, after each `;` to separate each part of the statement; after each `,`.

**New lines**: use new lines to separate blocks of code that perform logically related operations.

**Quotes** favor single quotes `'` instead of double quotes `"`. Double quotes are a standard in HTML attributes, so using single quotes helps remove problems when dealing with HTML strings. Use [template literals](/javascript-template-literals) when appropriate instead of variable interpolation.
