---
title: Work with HTTP headers in Express
description: "Learn how to access and change HTTP headers using Express"
date: 2018-09-19T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-headers
---

## Access HTTP headers values from a request

You can access all the HTTP headers using the `Request.headers` property:

```js
app.get('/', (req, res) => {
  console.log(req.headers)
})
```

Use the `Request.header()` method to access one individual request header value:

```js
app.get('/', (req, res) => {
  req.header('User-Agent')
})
```

## Change any HTTP header value of a response

You can change any HTTP header value using `Response.set()`:

```js
res.set('Content-Type', 'text/html')
```

There is a shortcut for the Content-Type header however:

```js
res.type('.html')
// => 'text/html'

res.type('html')
// => 'text/html'

res.type('json')
// => 'application/json'

res.type('application/json')
// => 'application/json'

res.type('png')
// => image/png:
```
