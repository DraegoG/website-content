---
title: Serving Static Assets with Express
description: "How to serve static assets directly from a folder in Express"
date: 2018-08-31T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-static-assets
---

It's common to have images, CSS and more in a `public` subfolder, and expose them to the root level:

```js
const express = require('express')
const app = express()

app.use(express.static('public'))

/* ... */

app.listen(3000, () => console.log('Server ready'))
```

If you have an `index.html` file in `public/`, that will be served if you now hit the root domain URL (`http://localhost:3000`)
