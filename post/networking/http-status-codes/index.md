---
title: The HTTP Status Codes List
description: "Every HTTP response comes with a status code that signals with a clear number information about how the request was processed"
date: 2018-10-08T07:00:00+02:00
tags: network
---

An HTTP status code is the first line in an HTTP response, that's sent from a server to the client.

This list will be useful if you are trying to find out why a server sent a particular status code, and see what does it mean, or if you are building the server and you are browsing for the perfect status code to return.

Status codes are expressed through 3-digit numbers, plus a short description.

The first digit of the number identifies the **response group**.

There are 5 groups:

- `1xx`: informational response - indicates that the request was received and understood
- `2xx`: successful response - indicates the action requested by the client was received, understood and accepted
- `3xx`: redirection - indicates the client must take additional action to complete the request
- `4xx`: client error - indicates there was an error, that seems to have been caused by the client
- `5xx`: server error - indicates that an error happened on the server

In the rest of the post I list all the useful status codes.

(I removed some technology-specific ones, like the WebDAV ones, and the ones very rarely used)

## Informational responses

Status code | Description
------------|------------
100 Continue | The server has received the request headers and the client should proceed to send the request body (in the case of a request for which a body needs to be sent; for example, a POST request). Sending a large request body to a server after a request has been rejected for inappropriate headers would be inefficient. To have a server check the request's headers, a client must send Expect: 100-continue as a header in its initial request and receive a 100 Continue status code in response before sending the body. If the client receives an error code such as 403 (Forbidden) or 405 (Method Not Allowed) then it shouldn't send the request's body. The response 417 Expectation Failed indicates that the request should be repeated without the Expect header as it indicates that the server doesn't support expectations (this is the case, for example, of HTTP/1.0 servers).
101 Switching Protocols | The client asked the server to switch protocols and the server has agreed to do so. [See RFC 7231#6.2.2](https://tools.ietf.org/html/rfc7231#section-6.2.2)

## Successful responses

Status code | Description
------------|------------
200 OK | This is the standard response for successful HTTP requests.
201 Created | Typically a response to a POST request. The request has been completed, and a new resource has been created.
202 Accepted | The request has been accepted for processing. There's nothing said about the actual processing, and the result of that, which might happen on a separate server, or batched.
203 Non-Authoritative Information | The original server returned a 200, and a transforming proxy between the client and the server changed the payload
204 No Content | The server successfully processed the request, but is not returning any content.
205 Reset Content | The server successfully processed the request, but is not returning any content. Similar to a 204 response, but the server requires that the client resets the document view (used to clear forms, for example)
206 Partial Content | In response to a `Range` request coming from the client, the server sends a partial content response. [See RFC 7233#4.1](https://tools.ietf.org/html/rfc7233#section-4.1)

## Redirection

Status code | Description
------------|------------
301 Moved Permanently | This and all future requests should be directed to the given URI. Only use with GET/HEAD requests, and `308 Permanent Redirect` for all the other methods.
302 Found | The resource is temporarily moved to a URL specified by the `Location` header. Only use with GET/HEAD requests, and `307 Temporary Redirect` for all the other methods.
303 See Other | After a POST or PUT request, points to the confirmation message in the `Location` header, accessible using a new GET request.
304 Not Modified | When the client uses the request headers `If-Modified-Since` or `If-None-Match`, this response status code indicates that the resource has not been modified.
307 Temporary Redirect | Similar to the `302` request, except it does not allow changing the HTTP method
308 Permanent Redirect | Similar to the `301` request, except it does not allow changing the HTTP method

## Client errors

Status code | Description
------------|------------
400 Bad Request | Due to a request error that was generated on the client, the server cannot process the request. Errors can include a malformed request, size too large to be handled, or others.
401 Unauthorized | Sent when authentication is required and the client is not authorized
403 Forbidden | The resource is not available for various reasons. If the reason is authentication, prefer the `401 Unauthorized` status code.
404 Not Found | The requested resource could not be found.
405 Method Not Allowed | The resource is not available through that HTTP method, but might be with another.
406 Not Acceptable | The client passed an `Accept` header with values that are not compatible with the server.
407 Proxy Authentication Required | Between the client and the server there is a proxy that requires authentication.
408 Request Timeout | The server timed out waiting for the request.
409 Conflict | Indicates that the request could not be processed because of conflict in the current state of the resource, such as an edit conflict between multiple simultaneous updates.
410 Gone | The resource is no longer available and will not be available again. More powerful than a 404, for example search engines interpret it as an indication to remove that resource from their index.
411 Length Required | The client needs to add a Content-Length header to the request, and it was required.
412 Precondition Failed | Returned if the client sent an `If-Unmodified-Since` or `If-None-Match` request header, and the server cannot satisfy that condition.
413 Payload Too Large | The request is larger than the server is willing or able to process.
414 URI Too Long | The URI provided was too long for the server to process.
415 Unsupported Media Type | The request entity has a media type which the server or resource does not support.
416 Range Not Satisfiable | The client has asked for a portion of the file using the `Range` header, but the server cannot supply that portion.
417 Expectation Failed | The server cannot meet the requirements of the `Expect` request header.
421 Misdirected Request | The request was directed at a server that is not able to produce a response (for example because of connection reuse).
426 Upgrade Required | The client should switch to a different protocol such as TLS/1.0, specified in the `Upgrade` header field.
428 Precondition Required | The server requires the request to contain a `If-Match` header.
429 Too Many Requests | The user has sent too many requests in a given amount of time. Used for rate limiting.
431 Request Header Fields Too Large | The request cannot be fulfilled because one or more headers, or the whole headers set, is too large.
451 Unavailable For Legal Reasons | The resource is not available due to legal reasons

## Server errors

Status code | Description
------------|------------
500 Internal Server Error | A generic server error message, given when an unexpected condition was encountered and no more specific message is suitable.
501 Not Implemented | The server either does not recognize the request method, or it lacks the ability to fulfil the request.
502 Bad Gateway | The server was acting as a gateway or proxy and received an invalid response from the upstream server.
503 Service Unavailable | The server is currently temporarily unavailable (because it is overloaded or down for maintenance).
504 Gateway Timeout | The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.
505 HTTP Version Not Supported | The server does not support the HTTP protocol version specified in the request.
