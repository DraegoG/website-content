---
title: Routing in Express
description: "Routing is the process of determining what should happen when a URL is called, or also which parts of the application should handle a specific incoming request."
date: 2018-09-06T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-routing
---

Routing is the process of determining what should happen when a URL is called, or also which parts of the application should handle a specific incoming request.

In the Hello World example we used this code

```js
app.get('/', (req, res) => { /* */ })
```

This creates a route that maps accessing the root domain URL `/` using the HTTP GET method to the response we want to provide.

### Named parameters

What if we want to listen for custom requests, maybe we want to create a service that accepts a string, and returns that uppercase, and we don't want the parameter to be sent as a query string, but part of the URL. We use named parameters:

```js
app.get('/uppercase/:theValue', (req, res) => res.send(req.params.theValue.toUpperCase()))
```

If we send a request to `/uppercase/test`, we'll get `TEST` in the body of the response.

You can use multiple named parameters in the same URL, and they will all be stored in `req.params`.

### Use a regular expression to match a path

You can use [regular expressions](https://flaviocopes.com/javascript-regular-expressions/) to match multiple paths with one statement:

```js
app.get(/post/, (req, res) => { /* */ })
```

will match `/post`, `/post/first`, `/thepost`, `/posting/something`, and so on.
