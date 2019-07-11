---
title: "The URL Object"
date: 2019-05-14T07:00:00+02:00
description: "Find out what is a URL object and how to use it"
tags: browser
---

URL is a namespace used to host 2 static methods used to manipulate URLs using Blobs:

- `URL.createObjectURL()`
- `URL.revokeObjectURL()`

Given a blob, you generate a URL to it using the `URL.createObjectURL()` function:

```js
const myURL = URL.createObjectURL(aBlob)
```

Once you have the blob URL, you can destroy it from memory using:

```js
URL.revokeObjectURL(myURL)
```

---

In addition to this, URL offers a very different functionality through its constructor, which can be used to create a URL. You can call it like this:

```js
const currentUrl = new URL(window.location.href)
```

Now `currentUrl` has a set of properties you can use to inspect the URL:

- `hash` the hash fragment
- `host` the domain + port
- `hostname` the domain
- `href` contains the entire URL
- `origin` scheme + domain + port
- `password`
- `pathname`
- `port`
- `protocol`
- `search`
- `searchParams`
- `username`

which are the usual parts of a URL.

You can alter any of those, except `origin` and `searchParams` which are read only, and generate a new URL string by calling the `toString()` method, or by referencing the `href` property.
