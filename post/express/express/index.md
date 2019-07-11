---
title: Express, a popular Node.js Framework
seotitle: Introduction to Express, a practical tutorial
description: "Express is a Node.js Web Framework. Node.js is an amazing tool for building networking services and applications. Express builds on top of its features to provide easy to use functionality that satisfy the needs of the Web Server use case."
date: 2018-05-27T07:00:00+02:00
updated: 2019-04-26T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express
---

<!-- TOC -->

- [Introduction to Express](#introduction-to-express)
- [Installation](#installation)
- [Hello World](#hello-world)
- [Learn the basics of Express by understanding the Hello World code](#learn-the-basics-of-express-by-understanding-the-hello-world-code)
- [Request parameters](#request-parameters)
- [Sending a response](#sending-a-response)
  - [Send a JSON response](#send-a-json-response)
  - [Use end() to send an empty response](#use-end-to-send-an-empty-response)
  - [Change any HTTP header value](#change-any-http-header-value)
  - [Set the cookies](#set-the-cookies)
  - [Set the HTTP response status](#set-the-http-response-status)
  - [Handling redirects](#handling-redirects)
  - [Send a file to be downloaded](#send-a-file-to-be-downloaded)
  - [Support for JSONP](#support-for-jsonp)
- [Routing](#routing)
  - [Named parameters](#named-parameters)
  - [Use a regular expression to match a path](#use-a-regular-expression-to-match-a-path)
- [Middleware](#middleware)
- [Serving static assets](#serving-static-assets)
- [Templating](#templating)
- [What's next?](#whats-next)

<!-- /TOC -->

## Introduction to Express

Express is a [Node.js](/nodejs/) Web Framework.

Node.js is an amazing tool for building networking services and applications.

Express builds on top of its features to provide easy to use functionality that satisfy the needs of the Web Server use case.

It's Open Source, free, easy to extend, very performant, and has lots and lots of pre-built packages you can just drop in and use, to perform all kind of things.

## Installation

You can install Express into any project with [npm](/npm/):

```
npm install express
```

or [Yarn](/yarn/):

```
yarn add express
```

Both commands will also work in an empty directory, to start up your project from scratch, although `npm` does not create a `package.json` file at all, and Yarn creates a basic one.

Just run `npm init` or `yarn init` if you're starting a new project from scratch.

## Hello World

We're ready to create our first Express Web Server.

Here is some code:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => res.send('Hello World!'))
app.listen(3000, () => console.log('Server ready'))
```

Save this to an `index.js` file in your project root folder, and start the server using

```
node index.js
```

You can open the browser to port 3000 on localhost and you should see the `Hello World!` message.

## Learn the basics of Express by understanding the Hello World code

Those 4 lines of code do a lot behind the scenes.

First, we import the `express` package to the `express` value.

We instantiate an application by calling its `app()` method.

Once we have the application object, we tell it to listen for GET requests on the `/` path, using the `get()` method.

There is a method for every HTTP **verb**: `get()`, `post()`, `put()`, `delete()`, `patch()`:

```js
app.get('/', (req, res) => { /* */ })
app.post('/', (req, res) => { /* */ })
app.put('/', (req, res) => { /* */ })
app.delete('/', (req, res) => { /* */ })
app.patch('/', (req, res) => { /* */ })
```

Those methods accept a callback function, which is called when a request is started, and we need to handle it.

We pass in an arrow function:

```js
(req, res) => res.send('Hello World!')
```

Express sends us two objects in this callback, which we called `req` and `res`, that represent the Request and the Response objects.

Request is the HTTP request. It can give us all the info about that, including the request parameters, the headers, the body of the request, and more.

Response is the HTTP response object that we'll send to the client.

What we do in this callback is to send the 'Hello World!' string to the client, using the `Response.send()` method.

This method sets that string as the body, and it closes the connection.

The last line of the example actually starts the server, and tells it to listen on port `3000`. We pass in a callback that is called when the server is ready to accept new requests.

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
.xhr | true if the request is an [XMLHttpRequest](/xhr/)

## Sending a response

In the Hello World example we used the `Response.send()` method to send a simple string as a response, and to close the connection:

```js
(req, res) => res.send('Hello World!')
```

If you pass in a string, it sets the `Content-Type` header to `text/html`.

if you pass in an object or an array, it sets the `application/json` `Content-Type` header, and parses that parameter into [JSON](/json/).

`send()` automatically sets the `Content-Length` HTTP response header.

`send()` also automatically closes the connection.

### Send a JSON response

The `Response.json()` method accepts an object or array, and converts it to JSON before sending it:

```js
res.json({ username: 'Flavio' })
```

### Use end() to send an empty response

An alternative way to send the response, without any body, it's by using the `Response.end()` method:

```js
res.end()
```

### Change any HTTP header value

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

### Set the cookies

Use the `Response.cookie()` method to manipulate your cookies.

Examples:

```js
res.cookie('username', 'Flavio')
```

This method accepts a third parameter which contains various options:

```js
res.cookie('username', 'Flavio', { domain: '.flaviocopes.com', path: '/administrator', secure: true })

res.cookie('username', 'Flavio', { expires: new Date(Date.now() + 900000), httpOnly: true })
```

The most useful parameters you can set are:

Value | Description
---------|----------
`domain` | 	the [cookie domain name](/cookies/#set-a-cookie-domain)
`expires` | set the [cookie expiration date](/cookies/#set-a-cookie-expiration-date). If missing, or 0, the cookie is a session cookie
`httpOnly` | 	set the cookie to be accessible only by the web server. See [HttpOnly](/cookies/#httponly)
`maxAge` | 	set the expiry time relative to the current time, expressed in milliseconds
`path` | 	the [cookie path](/cookies/#set-a-cookie-path). Defaults to /
`secure` | 	Marks the [cookie HTTPS only](/cookies/#secure)
`signed` | 	set the cookie to be signed
`sameSite` | Value of [`SameSite`](/cookies/#samesite)

A cookie can be cleared with

```js
res.clearCookie('username')
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

### Handling redirects

Redirects are common in Web Development. You can create a redirect using the `Response.redirect()` method:

```js
res.redirect('/go-there')
```

This creates a 302 redirect.

A 301 redirect is made in this way:

```js
res.redirect(301, '/go-there')
```

You can specify an absolute path (`/go-there`), an absolute url (`https://anothersite.com`), a relative path (`go-there`) or use the `..` to go back one level:

```js
res.redirect('../go-there')
res.redirect('..')
```

You can also redirect back to the Referer HTTP header value (defaulting to `/` if not set) using

```js
res.redirect('back')
```

### Send a file to be downloaded

The `Response.download()` method allows you to send a file attached to the request, and the browser instead of showing it in the page, it will save it to disk.

```js
res.download('/file.pdf')

res.download('/file.pdf', 'user-facing-filename.pdf')
```

### Support for JSONP

JSONP is a way to consume cross-origin APIs from client-side JavaScript.

You can support it in your API by using the `Response.jsonp()` method, which is like `Response.json()` but handles JSONP callbacks:

```js
res.jsonp({ username: 'Flavio' })
```

## Routing

In the Hello World example we used this code

```js
app.get('/', (req, res) => { /* */ })
```

This creates a route that maps accessing the root domain URL `/` to the response we want to provide.

### Named parameters

What if we want to listen for custom requests, maybe we want to create a service that accepts a string, and returns that uppercase, and we don't want the parameter to be sent as a query string, but part of the URL. We use named parameters:

```js
app.get('/uppercase/:theValue', (req, res) => res.send(req.params.theValue.toUpperCase()))
```

If we send a request to `/uppercase/test`, we'll get `TEST` in the body of the response.

You can use multiple named parameters in the same URL, and they will all be stored in `req.params`.

### Use a regular expression to match a path

You can use [regular expressions](/javascript-regular-expressions/) to match multiple paths with one statement:

```js
app.get(/post/, (req, res) => { /* */ })
```

will match `/post`, `/post/first`, `/thepost`, `/posting/something`, and so on.

## Middleware

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

## Serving static assets

It's common to have images, CSS and more in a `public` subfolder, and expose them to the root level:

```js
const express = require('express')
const app = express()

app.use(express.static('public'))

/* ... */

app.listen(3000, () => console.log('Server ready'))
```

If you have an `index.html` file in `public/`, that will be served if you now hit the root domain URL (`http://localhost:3000`)

## Templating

Express is capable of handling server-side templates.

Jade is the default template engine, but you can use many different template ones, including Pug, Mustache, EJS and more.

Say I don't like Jade (I don't), and I want to use Handlebars.

I can install it using `npm install hbs`.

Put an `about.hbs` template file in the `views/` folder:

```
Hello from {{name}}
```

and then use this Express configuration to serve it on `/about`:

```js
const express = require('express')
const app = express()
const hbs = require('hbs')

app.set('view engine', 'hbs')

app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})

app.listen(3000, () => console.log('Server ready'))
```

You can also **render a React application server-side**, using the [`express-react-views`](https://github.com/reactjs/express-react-views) package.

Start with `npm install express-react-views react react-dom`.

Now instead of requiring `hbs` we require `express-react-views` and use that as the engine, using `jsx` files:

```js
const express = require('express')
const app = express()

app.set('view engine', 'jsx')
app.engine('jsx', require('express-react-views').createEngine())

app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})

app.listen(3000, () => console.log('Server ready'))
```

Just put an `about.jsx` file in `views/`, and calling `/about` should present you an "Hello from Flavio" string:

```js
const React = require('react')

class HelloMessage extends React.Component {
  render() {
    return <div>Hello from {this.props.name}</div>
  }
}

module.exports = HelloMessage
```

## What's next?

Express has all the power of Node.js under the hoods.

You can do anything that you want now, including connecting to a database, using any kind of caching, Redis, using sockets and everything you can imagine doing on a server.

The sky is the limit.