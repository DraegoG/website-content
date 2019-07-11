---
title: Send files using Express
description: "Express provides a handy method to transfer a file as attachment: `Response.download()`"
date: 2018-09-04T07:00:00+02:00
tags: express
tags_weight: 5
path: express-send-files
---

Express provides a handy method to transfer a file as attachment: `Response.download()`.

Once a user hits a route that sends a file using this method, browsers will prompt the user for download.

The `Response.download()` method allows you to send a file attached to the request, and the browser instead of showing it in the page, it will save it to disk.

```js
app.get('/', (req, res) => res.download('./file.pdf'))
```

In the context of an app:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => res.download('./file.pdf'))
app.listen(3000, () => console.log('Server ready'))
```

You can set the file to be sent with a custom filename:

```js
res.download('./file.pdf', 'user-facing-filename.pdf')
```

This method provides a callback function which you can use to execute code once the file has been sent:

```js
res.download('./file.pdf', 'user-facing-filename.pdf', (err) => {
  if (err) {
    //handle error
    return
  } else {
    //do something
  }
})
```
