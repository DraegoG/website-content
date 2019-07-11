---
title: Memoization in JavaScript
description: "An introduction to memoization in JavaScript"
date: 2019-03-11T15:00:00+02:00
tags: js
---

Memoization is one technique that lets you speed up considerably your applications.

It is not a technique unique to JavaScript, although I tagged this post as "JavaScript" because I will provide some JS examples.

Memoization is the act of storing the result of a function call after we run it, in the function itself. The next time we call the function, instead of performing its "regular" execution once again, it just returns us the stored result.

It's **caching, for functions**.

Why is this useful?

Suppose our function takes 1 second to run, while caching lets us speed up the process to 2 milliseconds. There is a clear gain here.

Sounds pretty cool. Where is the catch?

Memoization works if the result of calling a function with the same set of arguments results in the same output. In other words, the function must be **pure**. Otherwise caching the result would not make sense.

So, database queries, network requests, writing to files and other non-pure operations cannot be optimized with memoization. For those, you will need to find other ways to optimize them. Or just live with their inefficiency, which sometimes is unavoidable.

Let's create one example:

```js
// Calculate the factorial of num
const fact = num => {
  if (!fact.cache) {
    fact.cache = {}
  }
  if (fact.cache[num] !== undefined) {
    console.log(num + ' cached')
    return fact.cache[num];
  } else {
    console.log(num + ' not cached')
  }
  fact.cache[num] = num === 0 ? 1 : num * fact(num - 1)
  return fact.cache[num]
}
```

calculating the factorial of a number. The first time `fact()` is run, it creates a `cache` object property on the function itself, where to store the result of its calculation.

Upon every call, if we don't find the result of the number in the `cache` object, we perform the calculation. Otherwise we just return that.

Try to run it. I made a Codepen to make it easy to test, which uses `document.write()` to print to the HTML page (first time I used `document.write()` in ages, but this time it was useful).

<p class="codepen" data-height="419" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="aMbbbP" style="height: 419px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" data-pen-title="Memoization example factorial">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/aMbbbP/">
  Memoization example factorial</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<p></p>

There are libraries that will add the memoization feature to any pure function, so you can skip the task of modifying the function itself, but you just decorate it with this functionality.

In particular I mention [fast-memoize](https://github.com/caiogondim/fast-memoize.js).

Lodash also has a [`memoize()` method](https://lodash.com/docs/4.17.11#memoize), if you are a Lodash fan.