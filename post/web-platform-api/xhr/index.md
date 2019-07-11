---
title: "XMLHttpRequest (XHR)"
description: "The introduction of XMLHttpRequest (XHR) in browsers have been a huge win for the Web Platform, in the mid 2000. Let's see how it works."
date: 2018-04-05T07:07:49+02:00
tags: network
---

<!-- TOC -->

- [Introduction](#introduction)
- [An example XHR request](#an-example-xhr-request)
- [Additional open() parameters](#additional-open-parameters)
- [`onreadystatechange`](#onreadystatechange)
- [Aborting an XHR request](#aborting-an-xhr-request)
- [Comparison with jQuery](#comparison-with-jquery)
- [Comparison with Fetch](#comparison-with-fetch)
- [Cross Domain Requests](#cross-domain-requests)
- [Uploading files using XHR](#uploading-files-using-xhr)

<!-- /TOC -->

## Introduction

The introduction of XMLHttpRequest (XHR) in browsers have been a huge win for the Web Platform, in the mid 2000.

Things that now look normal, back in the day looked like coming from the future. I'm thinking about GMail or Google Maps, for example, all based in great part on XHR.

XHR was invented at Microsoft in the nineties, and became a de-facto standard as all browsers implemented it in the 2002-2006 period, and the W3C standardized XMLHttpRequest in 2006.

As it sometimes happen in the Web Platform, initially there were a few inconsistencies that made working with XHR quite different cross-browser.

Libraries like jQuery got a boost of popularity by providing an easy to use abstraction for developers, and in turn helped spread the usage of this technology.

## An example XHR request

The following code creates an XMLHttpRequest (XHR) request object, and attaches a callback function that responds on the `onreadystatechange` event.

The xhr connection is set up to perform a GET request to `https://yoursite.com`, and it's started with the `send()` method:

```js
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    xhr.status === 200 ? console.log(xhr.responseText) : console.error('error')
  }
}
xhr.open('GET', 'https://yoursite.com')
xhr.send()
```

## Additional open() parameters

In the example above we just passed the method and the URL to the request.

We can specify the other HTTP methods of course (`get`, `post`, `head`, `put`, `delete`, `options`).

Other parameters let you specify a flag to make the request synchronous if set to false, and a set of credentials for HTTP authentication:

```js
open(method, url, asynchronous, username, password)
```

## `onreadystatechange`

The `onreadystatechange` is called multiple times during an XHR request. We explicitly ignore all the states other than `readyState === 4`, which means the request is done.

The states are

- 1 (OPENED): the request starts
- 2 (HEADERS_RECEIVED): the HTTP headers have been received
- 3 (LOADING): the response begins to download
- 4 (DONE): the response has been downloaded

## Aborting an XHR request

An XHR request can be aborted by calling the `abort()` method on the `xhr` object.

## Comparison with jQuery

With jQuery these lines can be translated to:

```js
$.get('https://yoursite.com', data => {
  console.log(data)
}).fail(err => {
  console.error(err)
})
```

## Comparison with Fetch

With the [Fetch API](/fetch-api/) this is the equivalent code:

```js
fetch('https://yoursite.com')
  .then(data => {
    console.log(data)
  })
  .catch(err => {
    console.error(err)
  })
```

## Cross Domain Requests

Note that an XMLHttpRequest connection is subject to specific limits that are enforced for security reasons.

One of the most obvious is the enforcement of the same origin policy.

You cannot access resources on another server, _unless_ the server explicitly supports this using [CORS (Cross Origin Resource Sharing)](/cors/).

## Uploading files using XHR

Check my tutorial on [how to upload files using XHR](/file-upload-using-ajax/).