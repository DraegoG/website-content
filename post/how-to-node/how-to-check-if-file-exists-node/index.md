---
title: "How to check if a file exists in Node.js"
date: 2018-09-26T07:00:00+02:00
description: "How to check if a file exists in the filesystem using Node.js, using the `fs` module"
tags: node
---

The way to check if a file exists in the filesystem, using Node.js, is by using the `fs.existsSync()` method:

```js
const fs = require('fs')

const path = './file.txt'

try {
  if (fs.existsSync(path)) {
    //file exists
  }
} catch(err) {
  console.error(err)
}
```

This method is synchronous. This means that it's blocking. To check if a file exists in an asynchronous way, you can use `fs.access()`, which checks the existence of a file without opening it:

```js
const fs = require('fs')

const path = './file.txt'

fs.access(path, fs.F_OK, (err) => {
  if (err) {
    console.error(err)
    return
  }

  //file exists
})
```
