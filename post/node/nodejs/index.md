---
title: Introduction to Node.js
date: 2018-03-22T07:07:09+02:00
updated: 2018-08-11T07:07:09+02:00
description: "This post is a getting started guide to Node.js, the server-side JavaScript runtime environment. Node.js is built on top of the Google Chrome V8 JavaScript engine, and it's mainly used to create web servers - but it's not limited to that"
tags: node
tags_weight: 4
path: node
---

<!-- TOC -->

- [Overview](#overview)
- [The best features of Node.js](#the-best-features-of-nodejs)
  - [Fast](#fast)
  - [Simple](#simple)
  - [JavaScript](#javascript)
  - [V8](#v8)
  - [Asynchronous platform](#asynchronous-platform)
  - [A huge number of libraries](#a-huge-number-of-libraries)
- [An example Node.js application](#an-example-nodejs-application)
- [Node.js frameworks and tools](#nodejs-frameworks-and-tools)

<!-- /TOC -->

Node.js is a **runtime environment for [JavaScript](https://flaviocopes.com/javascript/)** that runs on the **server**.

Node.js is open source, cross-platform, and since its introduction in 2009, it got hugely popular and now plays a significant role in the web development scene. If GitHub stars are one popularity indication factor, having 58000+ stars means being very popular.

Node.js runs the V8 JavaScript engine, the core of Google Chrome, outside of the browser. Node.js is able to leverage the work of the engineers that made (and will continue to make) the Chrome JavaScript runtime blazing fast, and this allows Node.js to benefit from the huge performance improvements and the Just-In-Time compilation that V8 performs. Thanks to this, JavaScript code running in Node.js can become very performant.

A Node.js app is run by a single process, without creating a new thread for every request. Node provides a set of asynchronous I/O primitives in its standard library that will prevent JavaScript code from blocking and generally, libraries in Node.js are written using non-blocking paradigms, making a blocking behavior an exception rather than the normal.

When Node.js needs to perform an I/O operation, like reading from the network, access a database or the filesystem, instead of blocking the thread Node.js will resume the operations when the response comes back, instead of wasting CPU cycles waiting.

This allows Node.js to handle thousands of concurrent connections with a single server without introducing the burden of managing threads concurrency, which would be a major source of bugs.

Node.js has a unique advantage because millions of frontend developers that write JavaScript for the browser are now able to run the server-side code and frontend-side code without the need to learn a completely different language.

In Node.js the new [ECMAScript](https://flaviocopes.com/ecmascript/) standards can be used without problems, as you don't have to wait for all your users to update their browsers - you are in charge of deciding which ECMAScript version to use by changing the Node.js version, and you can also enable specific experimental features by running Node with flags.

## Node.js has a huge number of libraries

[`npm`](https://flaviocopes.com/npm/) with its simple structure helped the ecosystem of node.js proliferate and now the npm registry hosts almost 500.000 open source packages you can freely use.

## An example Node.js application

The most common example Hello World of Node.js is a web server:

```js
const http = require('http')

const hostname = '127.0.0.1'
const port = 3000

const server = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/plain')
  res.end('Hello World\n')
})

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`)
})
```

To run this snippet, save it as a `server.js` file and run `node server.js` in your terminal.

This code first includes the Node.js [`http` module](https://nodejs.org/api/http.html).

Node.js has an amazing [standard library](https://nodejs.org/api/), including a first-class support for networking.

The `createServer()` method of `http` creates a new HTTP server and returns it.

The server is set to listen on the specified port and hostname. When the server is ready, the callback function is called, in this case informing us that the server is running.

Whenever a new request is received, the [`request` event](https://nodejs.org/api/http.html#http_event_request) is called, providing two objects: a request (an [`http.IncomingMessage`](https://nodejs.org/api/http.html#http_class_http_incomingmessage) object) and a response (an [`http.ServerResponse`](https://nodejs.org/api/http.html#http_class_http_serverresponse) object).

Those 2 objects are essential to handle the HTTP call.

The first provides the request details. In this simple example, this is not used, but you could access the request headers and request data.

The second is used to return data to the caller.

In this case with

```js
res.statusCode = 200
```

we set the statusCode property to 200, to indicate a successful response.

We set the Content-Type header:

```js
res.setHeader('Content-Type', 'text/plain')
```

and we end close the response, adding the content as an argument to `end()`:

```js
res.end('Hello World\n')
```

## Node.js frameworks and tools

Node.js is a low-level platform, and to make things easier and more interesting for developers thousands of libraries were built upon Node.js.

Many of those established over time as popular options. Here is a non-comprehensive list of the ones I consider very relevant and worth learning:

- [**Express**](https://expressjs.com/), one of the most simple yet powerful ways to create a web server. Its minimalist approach, unopinionated, focused on the core features of a server, is key to its success.
- [**Meteor**](https://flaviocopes.com/meteor/), an incredibly powerful full-stack framework, powering you with an isomorphic approach to building apps with JavaScript, sharing code on the client and the server. Once an off-the-shelf tool that provided everything, now integrates with frontend libs React, [Vue](https://flaviocopes.com/vue-introduction/) and Angular. Can be used to create mobile apps as well.
- [**koa**](http://koajs.com/), built by the same team behind Express, aims to be even simpler and smaller, building on top of years of knowledge. The new project born out of the need to create incompatible changes without disrupting the existing community.
- [**Next.js**](https://flaviocopes.com/nextjs/), a framework to render server-side rendered [React](https://flaviocopes.com/react/) applications.
- [**Micro**](https://github.com/zeit/micro), a very lightweight server to create asynchronous HTTP microservices.
- [**Socket.io**](https://socket.io/), a real-time communication engine to build network applications.
