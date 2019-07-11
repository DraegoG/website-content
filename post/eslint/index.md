---
title: Keep your code clean with ESLint
date: 2018-03-12T08:00:15+02:00
description: "Learn the basics of the most popular JavaScript linter, which can help to make your code adhere to a certain set of syntax conventions, check if the code contains possible sources of problems and if the code matches a set of standards you or your team define"
booktitle: ESLint
tags: devtools
---

<!-- TOC -->

- [What is linter?](#what-is-linter)
- [ESLint](#eslint)
- [Install ESLint globally](#install-eslint-globally)
- [Install ESLint locally](#install-eslint-locally)
- [Use ESLint in your favourite editor](#use-eslint-in-your-favourite-editor)
- [Common ESLint configurations](#common-eslint-configurations)
  - [Airbnb style guide](#airbnb-style-guide)
  - [React](#react)
  - [Use a specific version of ECMAScript](#use-a-specific-version-of-ecmascript)
  - [Force strict mode](#force-strict-mode)
  - [More advanced rules](#more-advanced-rules)
- [Disabling rules on specific lines](#disabling-rules-on-specific-lines)

<!-- /TOC -->

ESLint is a [JavaScript](/javascript/) linter.

## What is linter?

Good question! A linter is a tool that identifies issues in your code.

Running a linter against your code can tell you many things:

- if the code adheres to a certain set of syntax conventions
- if the code contains possible sources of problems
- if the code matches a set of standards you or your team define

It will raise warnings that you, or your tools, can analyze and give you actionable data to improve your code.

## ESLint

ESLint is a linter for the JavaScript programming language, written in [Node.js](/nodejs/).

It is hugely useful because JavaScript, being an interpreted language, does not have a compilation step and many errors are only possibly found at runtime.

ESLint will help you catch those errors. Which errors in particular you ask?

- avoid infinite [loops](/javascript-loops/) in the `for` loop conditions
- make sure all getter methods return something
- disallow console.log (and similar) statements
- check for duplicate cases in a switch
- check for unreachable code
- check for JSDoc validity

and much more! The full list is available at <https://eslint.org/docs/rules/>

> The growing popularity of [Prettier](/prettier/) as a code formatter made the styling part of ESLint kind of obsolete, but ESLint is still very useful to catch errors and code smells in your code.

ESLint is very flexible and configurable, and you can choose which rules you want to check for, or which kind of style you want to enforce. Many of the available rules are disabled and you can turn them on in your `.eslintrc` configuration file, which can be global or specific to your project.

## Install ESLint globally

Using [npm](/npm/).

```bash
npm install -g eslint

# create a `.eslintrc` configuration file
eslint --init

# run ESLint against any file with
eslint yourfile.js
```

## Install ESLint locally

```bash
npm install eslint --save-dev

# create a `.eslintrc` configuration file
./node_modules/.bin/eslint --init

# run ESLint against any file with
./node_modules/.bin/eslint yourfile.js
```

## Use ESLint in your favourite editor

The most common use of ESLint is within your editor of course.

## Common ESLint configurations

ESLint can be configured in tons of different ways.

### Airbnb style guide

A common setup is to use the [Airbnb JavaScript coding style](https://github.com/airbnb/javascript) to lint your code.

Run

```bash
yarn add --dev eslint-config-airbnb
```

or

```bash
npm install --save-dev eslint-config-airbnb
```

to install the Airbnb configuration package, and add in your `.eslintrc` file in the root of your project:

```json
{
  "extends": "airbnb",
}
```

### React

Linting React code is easy with the React plugin:

```bash
yarn add --dev eslint-plugin-react
```

or

```bash
npm install --save-dev eslint-plugin-react
```

In your `.eslintrc` file add

```json
{
  "extends": "airbnb",
  "plugins": [
      "react"
  ],
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    }
  }
}
```

### Use a specific version of ECMAScript

[ECMAScript](/ecmascript/) changes version every year now.

The default is currently set to 5, which means pre-2015.

Turn on ES6 (or higher) by setting this property in `.eslintrc`:

```json
{
  "parserOptions": {
    "ecmaVersion": 6,
  }
}
```

### Force strict mode


```json
{
  "parserOptions": {
    "ecmaFeatures": {
      "impliedStrict": true
    }
  }
}
```

### More advanced rules

A detailed guide on rules can be found on the official site at <https://eslint.org/docs/user-guide/configuring>

## Disabling rules on specific lines

Sometimes a rule might give a false positive, or you might be explicitly willing to take a route that ESLint flags.

In this case, you can disable ESLint entirely on a few lines:

```js
/* eslint-disable */
alert('test');
/* eslint-enable */
```

or on a single line:

```js
alert('test'); // eslint-disable-line
```

or just disable one or more specific rules for multiple lines:

```js
/* eslint-disable no-alert, no-console */
alert('test');
console.log('test');
/* eslint-enable no-alert, no-console */
```

or for a single line:

```js
alert('test'); // eslint-disable-line no-alert, quotes, semi
```