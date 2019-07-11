---
title: Parsing JSON with Node.js
description: "How to parse JSON from a string, and how to read a JSON file in Node.js"
date: 2018-08-07T15:00:00+02:00
tags: node
tags_weight: 21
path: node-parse-json
---

If you have [JSON](/json/) data as part of a string, the best way to parse it is by using the `JSON.parse` method that's part of the JavaScript standard since ECMAScript 5, and it's provided by [V8](https://flaviocopes.com/v8/), the JavaScript engine that powers [Node.js](https://flaviocopes.com/nodejs/).

Example:

```js
const data = '{ "name": "Flavio", "age": 35 }'
try {
  const user = JSON.parse(data)
} catch(err) {
  console.error(err)
}
```

Note that `JSON.parse` is synchronous, so the more the JSON file is big, the more time your program execution will be blocked until the JSON is finished parsing.

You can process the JSON asynchronously by wrapping it in a [promise](https://flaviocopes.com/javascript-promises/) and a setTimeout call, which makes sure parsing takes place in the next iteration of the event loop:

```js
const parseJsonAsync = (jsonString) => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(JSON.parse(jsonString))
    })
  })
}

const data = '{ "name": "Flavio", "age": 35 }'
parseJsonAsync(data).then(jsonData => console.log(jsonData))
```

If your JSON is in a file instead, you first have to read it.

A very simple way to do so is to use `require()`:

```js
const data = require('./file.json')
```

Since you used the `.json` extension, `require()` is smart enough to understand that, and parse the JSON in the `data` object.

One caveat is that file reading is synchronous. Plus, the result of the require() call is cached, so if you call it again because you updated the file, you won't get the new contents until the program exits.

This feature was provided to use a JSON file for the app configuration, and it's a perfectly valid use case.

You can also read the file manually, using `fs.readFileSync`:

```js
const fs = require('fs')
const fileContents = fs.readFileSync('./file.json', 'utf8')

try {
  const data = JSON.parse(fileContents)
} catch(err) {
  console.error(err)
}
```

This reads the file synchronously.

You can also read the file asynchronously using `fs.readFile`, and this is the best option. In this case, the file content is provided as a callback, and inside the callback you can process the JSON:

```js
const fs = require('fs')

fs.readFile('/path/to/file.json', 'utf8', (err, fileContents) => {
  if (err) {
    console.error(err)
    return
  }
  try {
    const data = JSON.parse(fileContents)
  } catch(err) {
    console.error(err)
  }
})
```
