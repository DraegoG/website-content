---
title: "The String replace() method"
description: "Find out all about the JavaScript replace() method of a string"
date: 2019-02-11T07:00:00+02:00
tags: js
---

Finds the _first_ occurrence of `str1` in the current string and replaces it with `str2`.

Returns a new string without mutating the original one.

```js
'JavaScript'.replace('Java', 'Type') //'TypeScript'
```

You can pass a [regular expression](/javascript-regular-expressions/) as the first argument:

```js
'JavaScript'.replace(/Java/, 'Type') //'TypeScript'
```

`replace()` will only replace the *first* occurrence, unless you use a regex as the search string, and you specify the global (`/g`) option:

```js
'JavaScript JavaX'.replace(/Java/g, 'Type') //'TypeScript TypeX'
```

The second parameter can be a function. This function will be invoked when the match is found (or for *every* match foundm if using a global regex `/g`), with a number of arguments:

- the the string that matches the pattern
- an integer that specifies the position within the string where the match occurred
- the string

The return value of the function will replace the matched part of the string.

Example:

```js
'JavaScript'.replace(/Java/, (match, index, originalString) => {
  console.log(match, index, originalString)
  return 'Test'
}) //TestScript
```

This also works for regular strings, not just regexes:

```js
'JavaScript'.replace('Java', (match, index, originalString) => {
  console.log(match, index, originalString)
  return 'Test'
}) //TestScript
```

In case your regex has **capturing groups**, those values will be passed as arguments right after the match parameter:

```js
'2015-01-02'.replace(/(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/, (match, year, month, day, index, originalString) => {
  console.log(match, year, month, day, index, originalString)
  return 'Test'
}) //Test
```
