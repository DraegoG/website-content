---
title: Retrieve the POST query parameters using Express
seotitle: How to retrieve the POST query parameters using Express
description: "Found out how to retrieve the POST query parameters using Express"
date: 2018-09-15T07:00:00+02:00
tags: express
tags_weight: 77
path: express-post-query-variables
---

POST query parameters are sent by HTTP clients for example by forms, or when performing a POST request sending data.

How can you access this data?

If the data was sent as [JSON](/json/), using `Content-Type: application/json`, you will use the `express.json()` middleware:

```js
const express = require('express')
const app = express()

app.use(express.json())
```

If the data was sent using `Content-Type: application/x-www-form-urlencoded`, you will use the `express.urlencoded()` middleware:

```js
const express = require('express')
const app = express()

app.use(express.urlencoded())
```

In both cases you can access the data by referencing it from `Request.body`:

```js
app.post('/form', (req, res) => {
  const name = req.body.name
})
```

> Note: older Express versions required the use of the `body-parser` module to process POST data. This is no longer the case as of Express 4.16 (released in September 2017) and later versions.