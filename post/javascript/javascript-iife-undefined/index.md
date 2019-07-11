---
title: "Passing undefined to JavaScript Immediately-invoked Function Expressions"
description: "Sometimes you can spot old code in the wild where `undefined` is passed to a function. Why?"
date: 2019-01-19T07:00:00+02:00
tags: js
---

I discovered this little trick while watching the famous [Paul Irish video about the jQuery source code](https://www.youtube.com/watch?v=i_qE1iAmjFg).

That video comes from a different era and it's 9 years old at the time of writing, and the jQuery source code has changed since, so you can't spot this thing in there, but it's still something I found interesting.

Also, JavaScript has since changed. This technique only applied to pre-ES5 JavaScript.

Before ES5, released in 2009, this was an almost required step.

> Note: ES5+ codebases do not need to add this any more because now `undefined` is a read-only value.

Sometimes in our code we do check variables to see if they are undefined, in this way:

```js
if (car !== undefined) {

}
```

If this is our code, that runs on our own servers, which we control, this should work fine. But imagine that a library like jQuery needs to be battle tested, to work on every possible site.

If someone overwrites `undefined` with a simple

```js
undefined = '🤔' //whatever value you prefer
```

then the above `if` would fail, comparing `car` to `🤔`.

This has since been fixed in ES5, but was possible before that.

If `car` was actually undefined, there was no way to find out now.

Except using this technique: we wrap all our code in an IIFE ([Immediately-invoked Function Expression](/javascript-iife/)) and we pass one parameter to the function definition, without adding it in the invocation phase.

```js
(function() {
  /* our function code */
})()
```

```js
(function(undefined) {
  /* our function code */
})()
```

See, `undefined` is passed as argument, but not passed as a parameter when we invoke the function. So, inside the function the value of the variable `undefined` is (guaranteed) the original value of `undefined`. No matter what other scripts on the page do to it, it's isolated.

Now, my favorite way to solve this problem is to use this technique to check for undefined values:

```js
if (typeof car !== 'undefined') {

}
```

The `typeof` operator returns a string with the type of a variable. We can check it against the `'undefined'` string, and we wouldn't have the above problem in the first place.

But it's always good to know the reasons about some things you can read on code written by others, especially when it's library-level code that need to run everywhere.