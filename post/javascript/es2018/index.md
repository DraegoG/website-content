---
title: The ES2018 Guide
description: "ECMAScript is the standard upon which JavaScript is based, and it's often abbreviated to ES. Discover everything about ECMAScript, and the features added in ES2018, aka ES9"
date: 2018-10-03T15:00:00+02:00
tags: js
tags_weight: 3
---

<!-- TOC -->

- [Rest/Spread Properties](#restspread-properties)
- [Asynchronous iteration](#asynchronous-iteration)
- [Promise.prototype.finally()](#promiseprototypefinally)
- [Regular Expression improvements](#regular-expression-improvements)
  - [RegExp lookbehind assertions: match a string depending on what precedes it](#regexp-lookbehind-assertions-match-a-string-depending-on-what-precedes-it)
  - [Unicode property escapes `\p{…}` and `\P{…}`](#unicode-property-escapes-p-and-p)
  - [Named capturing groups](#named-capturing-groups)
  - [The `s` flag for regular expressions](#the-s-flag-for-regular-expressions)

<!-- /TOC -->

ES2018 is the latest version of the [ECMAScript](/ecmascript/) standard.

What are the new things introduced in it?

## Rest/Spread Properties

[ES6](/es6/) introduced the concept of a **rest element** when working with **array destructuring**:

```js
const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
```

and **spread elements**:

```js
const numbers = [1, 2, 3, 4, 5]
const sum = (a, b, c, d, e) => a + b + c + d + e
const sumOfNumbers = sum(...numbers)
```

ES2018 introduces the same but for objects.

**Rest properties**:

```js
const { first, second, ...others } = { first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }

first // 1
second // 2
others // { third: 3, fourth: 4, fifth: 5 }
```

**Spread properties** allow to create a new object by combining the properties of the object passed after the [**spread operator**](/javascript-spread-operator/):

```js
const items = { first, second, ...others }
items //{ first: 1, second: 2, third: 3, fourth: 4, fifth: 5 }
```

## Asynchronous iteration

The new construct `for-await-of` allows you to use an async iterable object as the loop iteration:

```js
for await (const line of readLines(filePath)) {
  console.log(line)
}
```

Since this uses `await`, you can use it only inside `async` functions, like a normal `await` (see [async/await](/async-await/))

## Promise.prototype.finally()

When a promise is fulfilled, successfully it calls the `then()` methods, one after another.

If something fails during this, the `then()` methods are jumped and the `catch()` method is executed.

`finally()` allow you to run some code regardless of the successful or not successful execution of the promise:

```js
fetch('file.json')
  .then(data => data.json())
  .catch(error => console.error(error))
  .finally(() => console.log('finished'))
```

## Regular Expression improvements

### RegExp lookbehind assertions: match a string depending on what precedes it

This is a lookahead: you use `?=` to match a string that's followed by a specific substring:

```js
/Roger(?=Waters)/

/Roger(?= Waters)/.test('Roger is my dog') //false
/Roger(?= Waters)/.test('Roger is my dog and Roger Waters is a famous musician') //true
```

`?!` performs the inverse operation, matching if a string is **not** followed by a specific substring:

```js
/Roger(?!Waters)/

/Roger(?! Waters)/.test('Roger is my dog') //true
/Roger(?! Waters)/.test('Roger Waters is a famous musician') //false
```

Lookaheads use the `?=` symbol. They were already available.

**Lookbehinds**, a new feature, uses `?<=`.

```js
/(?<=Roger) Waters/

/(?<=Roger) Waters/.test('Pink Waters is my dog') //false
/(?<=Roger) Waters/.test('Roger is my dog and Roger Waters is a famous musician') //true
```

A lookbehind is negated using `?<!`:

```js
/(?<!Roger) Waters/

/(?<!Roger) Waters/.test('Pink Waters is my dog') //true
/(?<!Roger) Waters/.test('Roger is my dog and Roger Waters is a famous musician') //false
```

### Unicode property escapes `\p{…}` and `\P{…}`

In a regular expression pattern you can use `\d` to match any digit, `\s` to match any character that's not a white space, `\w` to match any alphanumeric character, and so on.

This new feature extends this concept to all Unicode characters introducing `\p{}` and is negation `\P{}`.

Any [unicode](/unicode/) character has a set of properties. For example `Script` determines the language family, `ASCII` is a boolean that's true for ASCII characters, and so on. You can put this property in the graph parentheses, and the regex will check for that to be true:

```js
/^\p{ASCII}+$/u.test('abc')   //✅
/^\p{ASCII}+$/u.test('ABC@')  //✅
/^\p{ASCII}+$/u.test('ABC🙃') //❌
```

`ASCII_Hex_Digit` is another boolean property, that checks if the string only contains valid hexadecimal digits:

```js
/^\p{ASCII_Hex_Digit}+$/u.test('0123456789ABCDEF') //✅
/^\p{ASCII_Hex_Digit}+$/u.test('h')                //❌
```

There are many other boolean properties, which you just check by adding their name in the graph parentheses, including `Uppercase`, `Lowercase`, `White_Space`, `Alphabetic`, `Emoji` and more:

```js
/^\p{Lowercase}$/u.test('h') //✅
/^\p{Uppercase}$/u.test('H') //✅

/^\p{Emoji}+$/u.test('H')   //❌
/^\p{Emoji}+$/u.test('🙃🙃') //✅
```

In addition to those binary properties, you can check any of the unicode character properties to match a specific value. In this example, I check if the string is written in the greek or latin alphabet:

```js
/^\p{Script=Greek}+$/u.test('ελληνικά') //✅
/^\p{Script=Latin}+$/u.test('hey') //✅
```

Read more about all the properties you can use [directly on the proposal](https://github.com/tc39/proposal-regexp-unicode-property-escapes).

### Named capturing groups

In ES2018 a [capturing group](/javascript-regular-expressions/#capturing-groups) can be assigned to a name, rather than just being assigned a slot in the result array:

```js
const re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/
const result = re.exec('2015-01-02')

// result.groups.year === '2015';
// result.groups.month === '01';
// result.groups.day === '02';
```

### The `s` flag for regular expressions

The `s` flag, short for _single line_, causes the `.` to match new line characters as well. Without it, the dot matches regular characters but not the new line:

```js
/hi.welcome/.test('hi\nwelcome') // false
/hi.welcome/s.test('hi\nwelcome') // true
```
