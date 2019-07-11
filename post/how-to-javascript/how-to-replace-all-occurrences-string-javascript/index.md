---
title: "How to replace all occurrences of a string in JavaScript"
date: 2018-07-02T07:06:15+02:00
updated: 2019-05-28T07:06:15+02:00
description: "Find out the proper way to replace all occurrences of a string in plain JavaScript, from regex to other approaches"
tags: js
---

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/7FcavNZnLAc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

## Using a regular expression

This simple regex will do the task:

```js
String.replace(/<TERM>/g, '')
```

This performs a **case sensitive** substitution.

Here is an example, where I substitute all occurrences of the word 'dog' in the string `phrase`:

```js
const phrase = 'I love my dog! Dogs are great'
const stripped = phrase.replace(/dog/g, '')

stripped //"I love my ! Dogs are great"
```

To perform a case insensitive replacement, use the `i` option in the regex:

```js
String.replace(/<TERM>/gi, '')
```

Example:

```js
const phrase = 'I love my dog! Dogs are great'
const stripped = phrase.replace(/dog/g, '')

stripped //"I love my ! s are great"
```

Remember that if the string contains some special characters, it won't play well with regular expressions, so the suggestion is to escape the string using this function (taken from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Using_Special_Characters)):

```js
const escapeRegExp = (string) => {
  return string.replace(/[.*+?^${}()|[\]\\]/g, '\\$&')
}
```

## Using split and join

An alternative solution, albeit slower than the regex, is using two JavaScript functions.

The first is `split()`, which truncates a string when it finds a pattern (case sensitive), and returns an array with the tokens:

```js
const phrase = 'I love my dog! Dogs are great'
const tokens = phrase.split('dog')

tokens //["I love my ", "! Dogs are great"]
```

Then you join the tokens in a new string, this time without any separator:

```js
const stripped = tokens.join('') //"I love my ! Dogs are great"
```

Wrapping up:

```js
const phrase = 'I love my dog! Dogs are great'
const stripped = phrase.split('dog').join('')
```
