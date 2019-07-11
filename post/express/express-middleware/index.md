---
title: Express Middleware
description: "A middleware is a function that hooks into the routing process, and performs some operation at some point, depending on what it want to do."
date: 2018-09-17T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-middleware
---

A middleware is a function that hooks into the routing process, and performs some operation at some point, depending on what it want to do.

It's commonly used to edit the request or response objects, or terminate the request before it reaches the route handler code.

It's added to the execution stack like this:

```js
app.use((req, res, next) => { /* */ })
```

This is similar to defining a route, but in addition to the Request and Response objects instances, we also have a reference to the _next_ middleware function, which we assign to the variable `next`.

We always call `next()` at the end of our middleware function, to pass the execution to the next handler, unless we want to prematurely end the response, and send it back to the client.

You typically use pre-made middleware, in the form of `npm` packages. A big list of the available ones is [here](https://expressjs.com/en/resources/middleware.html).

One example is `cookie-parser`, which is used to parse the cookies into the `req.cookies` object. You install it using `npm install cookie-parser` and you can use it like this:

```js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

app.get('/', (req, res) => res.send('Hello World!'))

app.use(cookieParser())
app.listen(3000, () => console.log('Server ready'))
```

You can also set a middleware function to run for specific routes only, not for all, by using it as the second parameter of the route definition:

```js
const myMiddleware = (req, res, next) => {
  /* ... */
  next()
}

app.get('/', myMiddleware, (req, res) => res.send('Hello World!'))
```

If you need to store data that's generated in a middleware to pass it down to subsequent middleware functions, or to the request handler, you can use the `Request.locals` object. It will attach that data to the current request:

```js
req.locals.name = 'Flavio'
```
