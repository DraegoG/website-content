---
title: "How to use Async and Await with Array.map()"
description: "Using async/await combined with map() can be a little tricky. Find out how."
date: 2018-10-11T07:00:00+02:00
tags: js
tags_weight: 29
---

You want to execute an async function inside a `map()` call, to perform an operation on every element of the array, and get the results back.

How can you do so?

This is the correct syntax:

```js
const list = [] //...an array filled with values

const functionWithPromise = item => { //a function that returns a promise
  return Promise.resolve('ok')
}

const anAsyncFunction = async item => {
  return await functionWithPromise(item)
}

const getData = async () => {
  return await Promise.all(list.map(item => anAsyncFunction(item)))
}

const data = getData()
console.log(data)
```

The main thing to notice is the use of `Promise.all()`, which resolves when all it's promises are resolved.

`list.map()` returns a list of promises, so in `result` we'll get the value when everything we ran is resolved.

Remember, we must wrap any code that calls `await` in an `async` function.

See the [promises article](/javascript-promises/) for more on promises, and the [async/await guide](/javascript-async-await/).