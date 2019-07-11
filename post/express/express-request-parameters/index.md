---
title: Express, Request Parameters
description: "A handy reference to all the request object properties and how to use them"
date: 2018-09-12T07:00:00+02:00
updated: 2019-04-26T07:00:00+02:00
tags: express
tags_weight: 5
path: express-request-parameters
---

## Request parameters

I mentioned how the Request object holds all the HTTP request information.

These are the main properties you'll likely use:

Property  | Description
----------|----------
.app      | holds a reference to the Express app object
.baseUrl  | the base path on which the app responds
.body     | contains the data submitted in the request body (must be parsed and populated manually before you can access it)
.cookies  | contains the cookies sent by the request (needs the `cookie-parser` middleware)
.hostname | the hostname as defined in the [Host HTTP header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Host) value
.ip       | the client IP
.method   | the HTTP method used
.params   | the route named parameters
.path     | the URL path
.protocol | the request protocol
.query    | an object containing all the query strings used in the request
.secure   | true if the request is secure (uses HTTPS)
.signedCookies | contains the signed cookies sent by the request (needs the `cookie-parser` middleware)
.xhr | true if the request is an [XMLHttpRequest](https://flaviocopes.com/xhr/)

## How to retrieve the GET query string parameters using Express

The query string is the part that comes after the URL path, and starts with a question mark `?`.

Example:

```txt
?name=flavio
```

Multiple query parameters can be added using `&`:

```txt
?name=flavio&age=35
```

How do you get those query string values in Express?

Express makes it very easy by populating the `Request.query` object for us:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  console.log(req.query)
})

app.listen(8080)
```

This object is filled with a property for each query parameter.

If there are no query params, it's an empty object.

This makes it easy to iterate on it using the for...in loop:

```js
for (const key in req.query) {
  console.log(key, req.query[key])
}
```

This will print the query property key and the value.

You can access single properties as well:

```js
req.query.name //flavio
req.query.age //35
```

## How to retrieve the POST query string parameters using Express

POST query parameters are sent by HTTP clients for example by forms, or when performing a POST request sending data.

How can you access this data?

If the data was sent as [JSON](/json/), using `Content-Type: application/json`, you will use the `express.json()` middleware:

```js
const express = require('express')
const app = express()

app.use(express.json())
```

If the data was sent as JSON, using `Content-Type: application/x-www-form-urlencoded`, you will use the `express.urlencoded()` middleware:

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