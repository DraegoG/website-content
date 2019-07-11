---
title: "How to get the current timestamp in JavaScript"
date: 2018-05-18T07:06:15+02:00
updated: 2019-06-03T07:06:15+02:00
description: "Find out the ways JavaScript offers you to generate the current UNIX timestamp"
tags: js
---

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/dOq9q-nCgLE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

The UNIX timestamp is an integer that represents **the number of seconds elapsed since January 1 1970**.

On UNIX-like machines, which include Linux and macOS, you can type `date +%s` in the terminal and get the UNIX timestamp back:

```bash
$ date +%s
1524379940
```

The current timestamp can be fetched by calling the `now()` method on the `Date` object:

```js
Date.now()
```

You could get the same value by calling

```js
new Date().getTime()

or

new Date().valueOf()
```

> Note: IE8 and below do not have the `now()` method on `Date`. Look for a polyfill if you need to support IE8 and below, or use `new Date().getTime()` if `Date.now` is undefined (as that's what a polyfill would do)

The timestamp in JavaScript is expressed in **milliseconds**.

To get the timestamp expressed in seconds, convert it using:

```js
Math.floor(Date.now() / 1000)
```

> Note: some tutorials use `Math.round()`, but that will approximate the the next second even if the second is not fully completed.

or, less readable:

```js
~~(Date.now() / 1000)
```

I've seen tutorials using

```js
+new Date
```

which might seem a weird statement, but it's perfectly correct JavaScript code. The _unary operator +_ automatically calls the `valueOf()` method on any object it is assigned to, which returns the timestamp (in milliseconds). The problem with this code is that you instantiate a new Date object that's immediately discarded.