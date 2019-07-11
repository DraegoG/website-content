---
title: Send a JSON response using Express
description: "How to serve JSON data using the Node.js Express library"
date: 2018-09-01T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-send-json-response
---

When you listen for connections on a route in Express, the callback function will be invoked on every network call with a Request object instance and a Response object instance.

Example:

```js
app.get('/', (req, res) => res.send('Hello World!'))
```

Here we used the `Response.send()` method, which accepts any string.

You can send [JSON](/json/) to the client by using `Response.json()`, a useful method.

It accepts an object or array, and converts it to JSON before sending it:

```js
res.json({ username: 'Flavio' })
```
