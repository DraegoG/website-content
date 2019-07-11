---
title: The HTTP Response Headers List
description: "Every HTTP response has a set of  headers. This post aims to list all those headers, and describe them"
date: 2018-07-29T07:07:09+02:00
tags: network
---

Every HTTP response can have a set of headers.

This post aims to list all those headers, and describe them.

<!-- TOC -->

- [Standard headers](#standard-headers)
  - [`Accept-Patch`](#accept-patch)
  - [`Accept-Ranges`](#accept-ranges)
  - [`Age`](#age)
  - [`Allow`](#allow)
  - [`Alt-Svc`](#alt-svc)
  - [`Cache-Control`](#cache-control)
  - [`Connection`](#connection)
  - [`Content-Disposition`](#content-disposition)
  - [`Content-Encoding`](#content-encoding)
  - [`Content-Language`](#content-language)
  - [`Content-Length`](#content-length)
  - [`Content-Location`](#content-location)
  - [`Content-Range`](#content-range)
  - [`Content-Type`](#content-type)
  - [`Date`](#date)
  - [`Delta-Base`](#delta-base)
  - [`ETag`](#etag)
  - [`Expires`](#expires)
  - [`IM`](#im)
  - [`Last-Modified`](#last-modified)
  - [`Link`](#link)
  - [`Location`](#location)
  - [`Pragma`](#pragma)
  - [`Proxy-Authenticate`](#proxy-authenticate)
  - [`Public-Key-Pins`](#public-key-pins)
  - [`Retry-After`](#retry-after)
  - [`Server`](#server)
  - [`Set-Cookie`](#set-cookie)
  - [`Strict-Transport-Security`](#strict-transport-security)
  - [`Trailer`](#trailer)
  - [`Transfer-Encoding`](#transfer-encoding)
  - [`Tk`](#tk)
  - [`Upgrade`](#upgrade)
  - [`Vary`](#vary)
  - [`Via`](#via)
  - [`Warning`](#warning)
  - [`WWW-Authenticate`](#www-authenticate)
- [[CORS](/cors/) headers](#corscors-headers)
- [Non-standard headers:](#non-standard-headers)
  - [`Content-Security-Policy`](#content-security-policy)
  - [`Refresh`](#refresh)
  - [`X-Powered-By`](#x-powered-by)
  - [`X-Request-ID`](#x-request-id)
  - [`X-UA-Compatible`](#x-ua-compatible)
  - [`X-XSS-Protection`](#x-xss-protection)

<!-- /TOC -->

## Standard headers

### `Accept-Patch`

`Accept-Patch: text/example;charset=utf-8`

Specifies which patch document formats this server supports

### `Accept-Ranges`

`Accept-Ranges: bytes`

What partial content range types this server supports via byte serving

### `Age`

`Age: 12`

The age the object has been in a proxy cache in seconds

### `Allow`

`Allow: GET, HEAD`

Valid methods for a specified resource. To be used for a 405 Method not allowed

### `Alt-Svc`

`Alt-Svc: http/1.1= "http2.example.com:8001"; ma=7200`

A server uses "Alt-Svc" header (meaning Alternative Services) to indicate that its resources can also be accessed at a different network location (host or port) or using a different protocol. When using [HTTP/2](/http-2/), servers should instead send an ALTSVC frame

### `Cache-Control`

`Cache-Control: max-age=3600`
`Cache-Control: no-cache, no-store, max-age=0, must-revalidate`

If `no-cache` is used, the `Cache-Control` header can tell the browser to never use a cached version of a resource without first checking the ETag value.

`max-age` is measured in seconds

The more restrictive `no-store` option tells the browser (and all the intermediary network devices) the not even store the resource in its cache:

```txt
Cache-Control: no-store
```

### `Connection`

`Connection: close`

Control options for the current connection and list of hop-by-hop response fields. Deprecated in HTTP/2

### `Content-Disposition`

`Content-Disposition: attachment; filename="file.txt"`

An opportunity to raise a "File Download" dialogue box for a known MIME type with binary format or suggest a filename for dynamic content. Quotes are necessary with special characters

### `Content-Encoding`

`Content-Encoding: gzip`

The type of encoding used on the data. See HTTP compression

### `Content-Language`

`Content-Language: en`

The natural language or languages of the intended audience for the enclosed content

### `Content-Length`

`Content-Length: 348`

The length of the response body expressed in 8-bit bytes

### `Content-Location`

`Content-Location: /index.htm`

An alternate location for the returned data

### `Content-Range`

`Content-Range: bytes 21010-47021/47022`

Where in a full body message this partial message belongs

### `Content-Type`

`Content-Type: text/html; charset=utf-8`

The MIME type of this content

### `Date`

`Date: Tue, 15 Nov 1994 08:12:31 GMT`

The date and time that the message was sent (in "HTTP-date" format as defined by RFC 7231)

### `Delta-Base`

`Delta-Base: "abc"`

Specifies the delta-encoding entity tag of the response

### `ETag`

`ETag: "737060cd8c284d8a[...]"`

An identifier for a specific version of a resource, often a message digest

### `Expires`

`Expires: Sat, 01 Dec 2018 16:00:00 GMT`

Gives the date/time after which the response is considered stale (in "HTTP-date" format as defined by RFC 7231)

### `IM`

`IM: feed`

Instance-manipulations applied to the response

### `Last-Modified`

`Last-Modified: Mon, 15 Nov 2017 12:00:00 GMT`

The last modified date for the requested object (in "HTTP-date" format as defined by RFC 7231)

### `Link`

`Link: </feed>; rel="alternate"`

Used to express a typed relationship with another resource, where the relation type is defined by RFC 5988

### `Location`

`Location: /pub/WWW/People.html`

Used in redirection, or when a new resource has been created

### `Pragma`

`Pragma: no-cache`

Implementation-specific fields that may have various effects anywhere along the request-response chain.

### `Proxy-Authenticate`

`Proxy-Authenticate: Basic`

Request authentication to access the proxy

### `Public-Key-Pins`

HTTP Public Key Pinning, announces hash of website's authentic TLS certificate

### `Retry-After`

`Retry-After: 120` `Retry-After: Fri, 07 Nov 2014 23:59:59 GMT`

If an entity is temporarily unavailable, this instructs the client to try again later. Value could be a specified period of time (in seconds) or a HTTP-date

### `Server`

`Server: Apache/2.4.1 (Unix)`

A name for the server

### `Set-Cookie`

`Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1`

An HTTP cookie

### `Strict-Transport-Security`

`Strict-Transport-Security: max-age=16070400; includeSubDomains`

A HSTS Policy informing the HTTP client how long to cache the HTTPS only policy and whether this applies to subdomains

### `Trailer`

`Trailer: Max-Forwards`

The Trailer general field value indicates that the given set of header fields is present in the trailer of a message encoded with chunked transfer coding

### `Transfer-Encoding`

`Transfer-Encoding: chunked`

The form of encoding used to safely transfer the entity to the user. Currently defined methods are: chunked, compress, deflate, gzip, identity. Deprecated in HTTP/2

### `Tk`

`Tk: ?`

Tracking Status header, value suggested to be sent in response to a DNT(do-not-track), possible values: "!" — under construction "?" — dynamic "G" — gateway to multiple parties "N" — not tracking "T" — tracking "C" — tracking with consent "P" — tracking only if consented "D" — disregarding DNT "U" — updated

### `Upgrade`

 `Upgrade: h2c, HTTPS/1.3, IRC/6.9, RTA/x11, websocket`

Ask the client to upgrade to another protocol. Deprecated in HTTP/2

### `Vary`

`Vary: Accept-Language` `Vary: *`

Tells downstream proxies how to match future request headers to decide whether the cached response can be used rather than requesting a fresh one from the origin server

### `Via`

`Via: 1.0 fred, 1.1 example.com (Apache/1.1)`

Informs the client of proxies through which the response was sent

### `Warning`

`Warning: 199 Miscellaneous warning`

A general warning about possible problems with the entity body

### `WWW-Authenticate`

`WWW-Authenticate: Basic`

Indicates the authentication scheme that should be used to access the requested entity

## [CORS](/cors/) headers

- `Access-Control-Allow-Origin`
- `Access-Control-Allow-Credentials`
- `Access-Control-Expose-Headers`
- `Access-Control-Max-Age`
- `Access-Control-Allow-Methods`
- `Access-Control-Allow-Headers`

## Non-standard headers:

### `Content-Security-Policy`

Helps to protect against XSS attacks. [See MDN for more details](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)

### `Refresh`

`Refresh: 10;http://www.example.org/`

Redirect to a URL after an arbitrary delay expressed in seconds

### `X-Powered-By`

`X-Powered-By: Brain/0.6b`

Can be used by servers to send their name and version

### `X-Request-ID`

Allows the server to pass a request ID that clients can send back to let the server correlate the request

### `X-UA-Compatible`

Sets which version of Internet Explorer compatibility layer should be used. Only used if you need to support IE8 or IE9. [See StackOverflow](https://stackoverflow.com/a/6771584/205039)

### `X-XSS-Protection`

Now replaced by the `Content-Security-Policy` header, used in older browsers to stop pages load when an XSS attack is detected
