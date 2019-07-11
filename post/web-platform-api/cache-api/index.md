---
title: The Cache API Guide
date: 2018-02-20T12:07:09+02:00
description: The Cache API is part of the Service Worker specification, and is a great way to have more power on resources caching.
booktitle: "Cache API"
tags: browser
---

<!-- TOC -->

- [Introduction](#introduction)
- [Detect if the Cache API is available](#detect-if-the-cache-api-is-available)
- [Initialize a cache](#initialize-a-cache)
- [Add items to the cache](#add-items-to-the-cache)
  - [`cache.add()`](#cacheadd)
  - [`cache.addAll()`](#cacheaddall)
  - [Manually fetch and add](#manually-fetch-and-add)
- [Retrieve an item from the cache](#retrieve-an-item-from-the-cache)
- [Get all the items in a cache](#get-all-the-items-in-a-cache)
- [Get all the available caches](#get-all-the-available-caches)
- [Remove an item from the cache](#remove-an-item-from-the-cache)
- [Delete a cache](#delete-a-cache)

<!-- /TOC -->

## Introduction

The Cache API is part of the Service Worker specification, and is a great way to have more power on resources caching.

It allows you to **cache URL-addressable resources**, which means assets, web pages, HTTP APIs responses.

It's **not** meant to cache individual chunks of data, which is the task of the **IndexedDB API**.

It's currently available in Chrome >= 40, Firefox >=39 and Opera >= 27.

Safari and Edge recently introduced support for it.

Internet Explorer does not support it.

Mobile support is good on Android, supported on the Android Webview and in Chrome for Android, while on iOS it's only available to Opera Mobile and Firefox Mobile users.

## Detect if the Cache API is available

The Cache API is exposed through the `caches` object. To detect if the API is implemented in the browser, just check for its existence using:

```js
if ('caches' in window) {
  //ok
}
```

## Initialize a cache

Use the `caches.open` API, which returns a [promise](/javascript-promises/) with a **cache object** ready to be used:

```js
caches.open('mycache').then(cache => {
  // you can start using the cache
})
```

`mycache` is a name that I use to identify the cache I want to initialize. It's like a variable name, you can use any name you want.

If the cache does not exist yet, `caches.open` creates it.

## Add items to the cache

The `cache` object exposes two methods to add items to the cache: `add` and `addAll`.

### `cache.add()`

`add` accepts a single URL, and when called it fetches the resource and caches it.

```js
caches.open('mycache').then(cache => {
  cache.add('/api/todos')
})
```

To allow more control on the fetch, instead of a string you can pass a **Request** object, part of the [Fetch API](/fetch-api) specification:

```js
caches.open('mycache').then(cache => {
  const options = {
    // the options
  }
  cache.add(new Request('/api/todos', options))
})
```

### `cache.addAll()`

`addAll` accepts an array, and returns a [promise](/javascript-promises/) when all the resources have been cached.

```js
caches.open('mycache').then(cache => {
  cache.addAll(['/api/todos', '/api/todos/today']).then(() => {
    //all requests were cached
  })
})
```

### Manually fetch and add

`cache.add()` automatically fetches a resource, and caches it.

The Cache API offers a more granular control on this via `cache.put()`. You are responsible for fetching the resource and then telling the Cache API to store a response:

```js
const url = '/api/todos'
fetch(url).then(res => {
  return caches.open('mycache').then(cache => {
    return cache.put(url, res)
  })
})
```

## Retrieve an item from the cache

`cache.match()` returns a **Response** object which contains all the information about the request and the response of the network request

```js
caches.open('mycache').then(cache => {
  cache.match('/api/todos').then(res => {
    //res is the Response Object
  })
})
```

## Get all the items in a cache

```js
caches.open('mycache').then(cache => {
  cache.keys().then(cachedItems => {
    //
  })
})
```

_cachedItems_ is an array of **Request** objects, which contain the URL of the resource in the `url` property.

## Get all the available caches

The `caches.keys()` method lists the keys of every cache available.

```js
caches.keys().then(keys => {
  // keys is an array with the list of keys
})
```

## Remove an item from the cache

Given a `cache` object, its `delete()` method removes a cached resource from it.

```js
caches.open('mycache').then(cache => {
  cache.delete('/api/todos')
})
```

## Delete a cache

The `caches.delete()` method accepts a cache identifier and when executed it wipes the cache and its cached items from the system.

```js
caches.delete('mycache').then(() => {
  // deleted successfully
})
```
