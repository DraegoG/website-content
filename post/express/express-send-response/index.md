---
title: Send a response using Express
description: "How to send a response back to the client using Express"
date: 2018-09-03T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-send-response
---

In the Hello World example we used the `Response.send()` method to send a simple string as a response, and to close the connection:

```js
(req, res) => res.send('Hello World!')
```

If you pass in a string, it sets the `Content-Type` header to `text/html`.

if you pass in an object or an array, it sets the `application/json` `Content-Type` header, and parses that parameter into [JSON](/json/).

`send()` automatically sets the `Content-Length` HTTP response header.

`send()` also automatically closes the connection.

### Use end() to send an empty response

An alternative way to send the response, without any body, it's by using the `Response.end()` method:

```js
res.end()
```

### Set the HTTP response status

Use the `Response.status()`:

```js
res.status(404).end()
```

or

```js
res.status(404).send('File not found')
```

`sendStatus()` is a shortcut:

```js
res.sendStatus(200)
// === res.status(200).send('OK')

res.sendStatus(403)
// === res.status(403).send('Forbidden')

res.sendStatus(404)
// === res.status(404).send('Not Found')

res.sendStatus(500)
// === res.status(500).send('Internal Server Error')
```
