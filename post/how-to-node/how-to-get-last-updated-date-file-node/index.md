---
title: How to get the last updated date of a file using Node.js
description: "Discover how to retrieve the last updated date of a file with Node.js"
date: 2018-10-12T07:00:00+02:00
tags: node
---

All the file functions in Node.js are provided by the `fs` module. This module exposes a method called `statSync()`, which gets the file details synchronously.

By calling it passing a file path (relative to the file location, or absolute), it will return an object that contains the `mtime` property.

That is a `Date` object instance that contains the file last modified date.

```js
const fs = require('fs')

const getFileUpdatedDate = (path) => {
  const stats = fs.statSync(path)
  return stats.mtime
}
```

Check out the [JavaScript Date guide](/javascript-dates/) to find out more how to handle the Date object, if you need.
