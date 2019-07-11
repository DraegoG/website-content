---
title: The HTTP protocol
description: A detailed description of how the HTTP protocol, and the Web, work
date: 2018-10-04T07:00:00+02:00
updated: 2018-10-20T09:06:15+02:00
tags: network
path: http
---

HTTP (_Hyper Text Transfer Protocol_) is one of the application protocols of TCP/IP, the suite of protocols that powers the Internet.

Let me fix that: it's not *one* of the protocols, it's the most successful and popular one, by all means.

HTTP is what makes the World Wide Web work, giving browsers a language to communicate to remote servers that host web pages.

HTTP was first standardized in 1991, as a result of the work that Tim Berners-Lee did at CERN, the European Center of Nuclear Research, since 1989.

The goal was to allow researchers to easily exchange and interlink their papers. It was meant as a way for the scientific community to work better.

Back then the internet main applications basically consisted in FTP (the File Transfer Protocol), Email and Usenet (newsgroups, today almost abandoned).

In 1993 Mosaic, the first graphical web browser, was released, and things skyrocketed from there.

The Web became the killer app of the Internet.

Over time the Web and the ecosystem around it have dramatically evolved, but the basics still remain. One example of evolution: HTTP now powers, in addition to web pages, REST APIs, one common way to programmatically access a service over the Internet.

HTTP got a minor revision in 1997 with HTTP/1.1, and in 2015 its successor, [HTTP/2](/http-2/), was standardized and it's now being implemented by the major Web Servers used across the globe.

The HTTP protocol is considered insecure, just like any other protocol (SMTP, FTP..) not served over an encrypted connection. This is why there is a big push nowadays towards using HTTPS, which is HTTP served over TLS.

That said, the building blocks of HTTP/2 and HTTPS have their roots in HTTP, and in this article I'll introduce how HTTP works.

## HTML documents

HTTP is the way **web browsers** like Chrome, Firefox, Edge and many others (also called _clients_ from here on) communicate with **web servers**.

The name Hyper Text Transfer Protocol derives from the need of transferring not just files, like in FTP - the "File Transfer Protocol", but hypertexts, which would be written using HTML, and then represented graphically by the browser with a nice presentation and interactive links.

Links were the driving force that drove adoption, along with the ease of creation of new web pages.

HTTP is what transfer those hypertext files (and as we'll see also images and other file types) over the network.

## Hyperlinks

Inside a web browser, a document can point to another document using links.

A link is composed by a first part that determines the protocol and the server address, either through a domain name or an IP.

This part is not unique to HTTP, of course.

Then there's the document part. Anything appended to the address part represents the document path.

For example, this document address is `https://flaviocopes.com/http/`:

- `https` is the protocol.
- `flaviocopes.com` is the domain name that points to my server
- `/http/` is the document URL relative to the server root path.

The path can be nested: `https://flaviocopes.com/page/privacy/` and in this case the document URL is `/page/privacy`.

The web server is responsible for interpreting the request and, once analyzed, serving the correct response.

## A request

What's in a request?

The first thing is **the URL**, which we've already seen before.

When we enter an address and press enter in our browser, under the hoods the server sends to the correct IP address a request like this:

```
GET /a-page
```

where /a-page is the URL you requested.

The second thing is **the HTTP method** (also called verb).

HTTP in the early days defined 3 of them:

- `GET`
- `POST`
- `HEAD`

and HTTP/1.1 introduced

- `PUT`
- `DELETE`
- `OPTIONS`
- `TRACE`

We'll see them in detail in a minute.

The third thing that composes a request is a set of **HTTP headers**.

Headers are a set of `key: value` pairs that are used to communicate to the server-specific information that is predefined, so the server can know what we mean.

I described them in detail in [the HTTP request headers list](/http-request-headers/).

Give that list a quick look. All of those headers are optional, except `Host`.

## HTTP methods

### `GET`

GET is the most used method here. It's the one that's used when you type an URL in the browser address bar, or when you click a link.

It asks the server to send the requested resource as a response.

### `HEAD`

HEAD is just like GET, but tells the server to not send the response body back. Just the headers.

### `POST`

The client uses the POST method to send data to the server. It's typically used in forms, for example, but also when interacting with a REST API.

### `PUT`

The PUT method is intended to create a resource at that specific URL, with the parameters passed in the request body. Mainly used in REST APIs

### `DELETE`

The DELETE method is called against an URL to request deletion of that resource. Mainly used in REST APIs

### `OPTIONS`

When a server receives an OPTIONS request it should send back the list of HTTP methods allowed for that specific URL.

### `TRACE`

Returns back to the client the request that has been received. Used for debugging or diagnostic purposes.

## HTTP Client/Server communication

HTTP, as most of the protocols that belong to the TCP/IP suite, is a _stateless_ protocol.

Servers have no idea what's the current state of the client. All they care about is that they get request and they need to fulfill them.

Any prior request is meaningless in this context, and this makes it possible for a web server to be very fast, as there's less to process, and also it gives it bandwidth to handle a lot of concurrent requests.

HTTP is also very lean, and communication is very fast in terms of overhead.  This contrasts with the protocols that were the most used at the time HTTP was introduced: TCP and POP/SMTP, the mail protocols, which involve lots of handshaking and confirmations on the receiving ends.

Graphical browsers abstract all this communication, but we'll illustrate it here for learning purposes.

A message is composed by a first line, which starts with the HTTP method, then contains the resource relative path, and the protocol version:

```
GET /a-page HTTP/1.1
```

After that, we need to add the HTTP request headers. As mentioned above, there are many headers, but the only mandatory one is `Host`:

```
GET /a-page HTTP/1.1
Host: flaviocopes.com
```

How can you test this? Using **telnet**. This is a command-line tool that lets us connect to any server and send it commands.

Open your terminal, and type `telnet flaviocopes.com 80`

This will open a terminal, that tells you

```txt
Trying 178.128.202.129...
Connected to flaviocopes.com.
Escape character is '^]'.
```

You are connected to the Netlify web server that powers my blog. You can now type:

```
GET /axios/ HTTP/1.1
Host: flaviocopes.com

```

and press enter on an empty line to fire the request.

The response will be:

```txt
HTTP/1.1 301 Moved Permanently
Cache-Control: public, max-age=0, must-revalidate
Content-Length: 46
Content-Type: text/plain
Date: Sun, 29 Jul 2018 14:07:07 GMT
Location: https://flaviocopes.com/axios/
Age: 0
Connection: keep-alive
Server: Netlify

Redirecting to https://flaviocopes.com/axios/
```

See, this is an HTTP response we got back from the server. It's a 301 Moved Permanently request. See [the HTTP status codes list](/http-status-codes/) to know more about the status codes.

It basically tells us the resource has permanently moved to another location.

Why? Because we connected to port 80, which is the default for HTTP, but on my server I set up an automatic redirection to HTTPS.

The new location is specified in the `Location` HTTP response header.

There are other headers, all described in [the HTTP response headers list](/http-response-headers/).

In both the request and the response, an empty line separates the request header from the request body. The response body in this case contains the string

```
Redirecting to https://flaviocopes.com/axios/
```

which is 46 bytes long, as specified in the `Content-Length` header. It is shown in the browser when you open the page, while it automatically redirects you to the correct location.

In this case we're using telnet, the low-level tool that we can use to connect to any server, so we can't have any kind of automatic redirect.

Let's do this process again, now connecting to port 443, which is the default port of the HTTPS protocol. We can't use telnet because of the SSL handshake that must happen.

Let's keep things simple and use `curl`, another command-line tool. We cannot directly type the HTTP request, but we'll see the response:

```bash
curl -i https://flaviocopes.com/axios/
```

this is what we'll get in return:

```txt
HTTP/1.1 200 OK
Cache-Control: public, max-age=0, must-revalidate
Content-Type: text/html; charset=UTF-8
Date: Sun, 29 Jul 2018 14:20:45 GMT
Etag: "de3153d6eacef2299964de09db154b32-ssl"
Strict-Transport-Security: max-age=31536000
Age: 152
Content-Length: 9797
Connection: keep-alive
Server: Netlify

<!DOCTYPE html>
<html prefix="og: http://ogp.me/ns#" lang="en">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<title>HTTP requests using Axios</title>
....
```

I cut the response, but you can see that the HTML of the page is being returned now.

## Other resources

An HTTP server will not just transfer HTML files, but typically it will also serve other files: CSS, JS, SVG, PNG, JPG, lots of different file types.

This depends on the configuration.

HTTP is perfectly capable of transferring those files as well, and the client will know about the file type, thus interpret them in the right way.

This is how the web works: when an HTML page is retrieved by the browser, it's interpreted and any other resource it needs to display property (CSS, JavaScript, images..) is retrieved through additional HTTP requests to the same server.