---
title: Caching in HTTP
description: A detailed description of the caching options available through the HTTP protocol
date: 2018-10-07T07:00:00+02:00
tags: network
---

Caching is a technique that can help network connections be faster, because the less things need to be transferred, the better.

Many resources can be very large, and be very expensive in terms of time and also actual cost (on mobile, for example) to retrieve.

There are different caching strategies that are made available by HTTP and used by browsers.

<!-- TOC -->

- [No caching](#no-caching)
- [The `Expires` header](#the-expires-header)
- [Conditional GET](#conditional-get)
  - [Using `If-Modified-Since` and `Last-Modified`](#using-if-modified-since-and-last-modified)
  - [Using `If-None-Match` and `ETag`](#using-if-none-match-and-etag)

<!-- /TOC -->

## No caching

First, the `Cache-Control` header can tell the browser to never use a cached version of a resource without first checking the ETag value (more on this later), by using the `no-cache` value:

```txt
Cache-Control: no-cache
```

A more restrictive `no-store` option tells the browser (and all the intermediary network devices) the not even store the resource in its cache:

```txt
Cache-Control: no-store
```

If `Cache-Control` has the `max-age` value, that's used to determine the number of seconds this resource is valid as a cache:

```txt
Cache-Control: max-age=3600
```

## The `Expires` header

When an HTTP request is sent, the browser checks if it has a copy of that page in the cache, based on the URL you required.

If there is, it checks the page for _freshness_.

A page is fresh if the [HTTP response `Expires` header](/http-response-headers/#expires) value is less than the current datetime.

The Expires header takes this form:

```txt
Expires: Sat, 01 Dec 2018 16:00:00 GMT
```

## Conditional GET

There are different ways to perform a conditional get. All are based on using the `If-*` request headers:

- using `If-Modified-Since` and `Last-Modified`
- using `If-None-Match` and `ETag`

### Using `If-Modified-Since` and `Last-Modified`

The browser can send a request to the server and instead of just asking for the page, it adds an [`If-Modified-Since` header](/http-request-headers/#if-modified-since), based on the `Last-Modified` header value it got from the currently cached page.

This tells the server to only return a response body (the page content) if the resource has been updated since that date.

Otherwise the server returns a `304 Not Modified` response.

### Using `If-None-Match` and `ETag`

The Web Server (depending on the setup, how page are served, etc) can send an [ETag header](/http-response-headers/#etag).

That is the identifier of a resource. Every time the resource changes, for example it's updated, the ETag should change as well.

It's like a checksum.

The browser sends an [`If-None-Match` header](/http-request-headers/#if-none-match) that contains one (or more) ETag value.

If none match, the server returns the fresh version of the resource, otherwise a `304 Not Modified` response.