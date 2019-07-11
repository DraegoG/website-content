---
title: How to make your JavaScript functions sleep
date: 2018-07-23T07:07:09+02:00
description: "Learn how to make your function sleep for a certain amount of time in JavaScript"
tags: js
tags_weight: 42
---

Sometimes you want your function to pause execution for a fixed amount of seconds or milliseconds.

In a programming language like C or PHP, you'd call `sleep(2)` to make the program halt for 2 seconds. Java has `Thread.sleep(2000)`, Python has `time.sleep(2)`, Go has `time.Sleep(2 * time.Second)`.

JavaScript does not have a native sleep function, but thanks to the introduction of promises (and async/await in ES2018) we can implement such feature in a very nice and readable way, to make your functions sleep:

```js
const sleep = (milliseconds) => {
  return new Promise(resolve => setTimeout(resolve, milliseconds))
}
```

You can now use this with the `then` callback:

```js
sleep(500).then(() => {
  //do stuff
})
```

Or use it in an async function:

```js
const doSomething = async () => {
  await sleep(2000)
  //do stuff
}

doSomething()
```

Remember that due to how JavaScript works (read more about [the event loop](https://flaviocopes.com/javascript-event-loop/)), this does not pause the entire program execution like it might happen in other languages, but instead only your function sleeps.