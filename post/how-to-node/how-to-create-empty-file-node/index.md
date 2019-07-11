---
title: How to create an empty file in Node.js
description: "Discover how create an empty file in a filesystem folder in Node.js"
date: 2018-10-09T07:00:00+02:00
tags: node
---

The method `fs.openSync()` provided by the `fs` built-in module is the best way.

It returns a file descriptor:

```js
const fs = require('fs')
const filePath = './.data/initialized'

const fd = fs.openSync(filePath, 'w')
```

the `w` flag makes sure the file is created if not existing, and if the file exists it overwrites it with a new file, overriding its content.

Use the `a` flag to avoid overwriting. The file is still created if not existing.

If you don't need the file descriptor, you can wrap the call in a `fs.closeSync()` call, to close the file:

```js
const fs = require('fs')
const filePath = './.data/initialized'

fs.closeSync(fs.openSync(filePath, 'w'))
```
