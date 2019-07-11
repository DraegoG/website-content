---
title: "The JSONP Guide"
date: 2018-11-15T07:00:00+02:00
description: "JSONP is a way to load data from 3rd party servers, bypassing the same-origin policy"
tags: js
---

By default you can't load a [JSON](/json/) file from a domain and port that's not the current one, and use it in your application.

You might serve the app from `localhost:8080`, but the API is served by another Node.js application running on `localhost:2001`.

Or you might want to access some publicly available API served as JSON, in the browser.

This is a common need to consume APIs, but in the browser we're limited as for security reasons, because of the **Same-Origin Policy** this behavior must be denied by default to prevent possible issues.

JSONP was born before [CORS](/cors/) existed. Today, CORS is a more (the only one?) sensible approach to the problem, but it's useful to also know JSONP which might be better in your case. Also, some security issues were discovered around JSONP since its inception, so you need to know about all the [security implications of using JSONP](https://stackoverflow.com/questions/613962/is-jsonp-safe-to-use).

JSONP only supports the GET [HTTP](https://flaviocopes.com/http/) method, so it's much less capable than CORS.

## How does it work

A server must have support for JSONP, for example Express allows you to use the `Response.jsonp()` method, which is like `Response.json()` but handles JSONP callbacks:

```js
res.jsonp({ username: 'Flavio' })
```

On the client side, you load the endpoint specifying a callback function:

```js
<script src="http://localhost:2001/api.json?callback=theCallbackFunction"></script>
```

The callback function must be a global that will receive the JSON data:

```js
const theCallbackFunction = (data) => {
  console.log(data)
}
```

jQuery had a handy way of simplifying this approach by abstracting JSONP in its `ajax()` method:

```js
$.ajax({
  url: 'http://localhost:2001/api.json',
  dataType: 'jsonp',
  success: (data) => {
    console.log(data)
  }
})
```
