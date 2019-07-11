---
title: How to remove a file with Node.js
description: "Discover how to remove a file from the filesystem with Node.js"
date: 2018-10-10T07:00:00+02:00
tags: js
---

How do you remove a file from the filesytem using Node.js?

Node offers a synchronous method, and an asynchronous method through the `fs` built-in module.

The asynchronous one is `fs.unlink()`.

The synchronous one is `fs.unlinkSync()`.

The difference is simple: the synchronous call will cause your code to block and wait until the file has been removed. The asynchronous one will not block your code, and will call a callback function once the file has been deleted.

Here's how to use those 2 functions:

`fs.unlinkSync()`:

```js
const fs = require('fs')

const path = './file.txt'

try {
  fs.unlinkSync(path)
  //file removed
} catch(err) {
  console.error(err)
}
```

`fs.unlink()`:

```js
const fs = require('fs')

const path = './file.txt'

fs.unlink(path, (err) => {
  if (err) {
    console.error(err)
    return
  }

  //file removed
})
```
