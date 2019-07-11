---
title: "Semicolons in JavaScript"
description: "JavaScript semicolons are optional. I personally like avoiding using semicolons in my code, but many people prefer them."
date: 2018-07-16T07:06:29+02:00
booktitle: Semicolons
tags: js
tags_weight: 10
---

Semicolons in JavaScript divide the community. Some prefer to use them always, no matter what. Others like to avoid them.

After using semicolons for years, in the fall of 2017 I decided to try avoiding them as needed, and I did set up Prettier to automatically remove semicolons from my code, unless there is a particular code construct that requires them.

Now I find it natural to avoid semicolons, I think the code looks better and it's cleaner to read.

This is all possible because JavaScript does not strictly require semicolons. When there is a place where a semicolon was needed, it adds it behind the scenes.

The process that does this is called **Automatic Semicolon Insertion**.

It's important to know the rules that power semicolons, to avoid writing code that will generate bugs because does not behave like you expect.

## The rules of JavaScript Automatic Semicolon Insertion

The JavaScript parser will automatically add a semicolon when, during the parsing of the source code, it finds these particular situations:

1. when the next line starts with code that breaks the current one (code can spawn on multiple lines)
2. when the next line starts with a `}`, closing the current block
3. when the end of the source code file is reached
4. when there is a `return` statement on its own line
5. when there is a `break` statement on its own line
6. when there is a `throw` statement on its own line
7. when there is a `continue` statement on its own line

## Examples of code that does not do what you think

Based on those rules, here are some examples.

Take this:

```js
const hey = 'hey'
const you = 'hey'
const heyYou = hey + ' ' + you

['h', 'e', 'y'].forEach((letter) => console.log(letter))
```

You'll get the error `Uncaught TypeError: Cannot read property 'forEach' of undefined` because based on rule `1` JavaScript tries to interpret the code as

```js
const hey = 'hey';
const you = 'hey';
const heyYou = hey + ' ' + you['h', 'e', 'y'].forEach((letter) => console.log(letter))
```

---

Such piece of code:

```js
(1 + 2).toString()
```

prints `"3"`.

```js
const a = 1
const b = 2
const c = a + b
(a + b).toString()
```

instead raises a `TypeError: b is not a function` exception, because JavaScript tries to interpret it as

```js
const a = 1
const b = 2
const c = a + b(a + b).toString()
```

---

Another example based on rule 4:

```js
(() => {
  return
  {
    color: 'white'
  }
})()
```

You'd expect the return value of this immediately-invoked function to be an object that contains the `color` property, but it's not. Instead, it's `undefined`, because JavaScript inserts a semicolon after `return`.

Instead you should put the opening bracket right after `return`:

```js
(() => {
  return {
    color: 'white'
  }
})()
```

---

You'd think this code shows '0' in an alert:

```js
1 + 1
-1 + 1 === 0 ? alert(0) : alert(2)
```

but it shows 2 instead, because JavaScript per rule 1 interprets it as:

```js
1 + 1 -1 + 1 === 0 ? alert(0) : alert(2)
```

## Conclusion

Be careful. Some people are very opinionated on semicolons. I don't care honestly, the tool gives us the option not to use it, so we can avoid semicolons.

I'm not suggesting anything, other than picking your own decision.

We just need to pay a bit of attention, even if most of the times those basic scenarios never show up in your code.

Pick some rules:

- be careful with `return` statements. If you return something, add it on the same line as the return (same for `break`, `throw`, `continue`)
- never start a line with parentheses, those might be concatenated with the previous line to form a function call, or array element reference

And ultimately, always test your code to make sure it does what you want