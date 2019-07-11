---
title: The HTTP/2 protocol
description: A detailed description of how the HTTP/2 protocol works
date: 2018-12-11T07:00:00+02:00
tags: network
---

> I suggest to read the [HTTP tutorial](/http/) first

HTTP/2 is the current version of the HTTP protocol. Released in 2015 by the IETF (Internet Engineering Task Force) committee, it's now widely adopted thanks to its unique features.

HTTP/2 is way more performant than HTTP/1.1, the last version of HTTP that was available at the time.

The speed bump offered by HTTP/2 was so inviting that it was very quickly adopted - with a simple change in the Web Server (since HTTP/2 is 100% backwards compatible with HTTP/1.1), your websites and web apps now are working much faster automatically, which in turn is beneficial for your users and also for SEO purposes (as speed is a crucial factor for ranking).

How can HTTP/2 be much faster than HTTP/1.1? The reasons are many, all oriented towards reducing the inefficiencies of the previous version, and introducing features that can allow browsers to be more capable of serving resources quicker.

The main features of the new version of the protocol are:

- request and response multiplexing
- efficient compression of HTTP headers
- server push
- binary communication

## Multiplexing

Before HTTP/2, only one response could be served at a time per each TCP connection.

> TCP is the underlying protocol on top of which HTTP is built. TCP stays at the transport layer, while HTTP at the application level.

HTTP/2 enabled request/response multiplexing on top of a single TCP connection, allowing the server to serve multiple requests with the same connection resulting in a much faster communication.

This is the single change that will be a great benefit for your application, and makes several optimization techniques obsolete, including image sprites (which is used to combine several images in a single one, which is then "demultiplexed" by using a special CSS technique) and domain sharding, another hack used to prevent the browser limit of number of simultaneous connections to the same domain.

## Headers compression

HTTP Headers on pages and resources can grow quite big, considering a normal use of cookies and other header values. Compression enables HTTP to have a lighter footprint, reducing the amount of data exchanged between the client and the server.

## Server push

Server push is a feature that allows to send multiple responses to a single request. Since the server knows that when requesting a resource a client will then request other complementary resources (think CSS, JS, images linked to a page) a server can decide to send them immediately.

Instead of sending the HTML, waiting for the browser to parse it and fire other requests to get the assets, the server can push them altogether.

A server can also decide to send resources that might be needed in future requests, pre-optimizing the next page load and putting it in the client cache.

> Note that server push can have its own drawbacks as well - for example, you can risk sending too much data to the client that might not be needed (maybe it's already available on the client as cached), so use with caution

## Binary communication

HTTP/1.1 used text-based communication. HTTP/2 uses binary communication, which has a few advantages, including being more efficient to parse, less error prone and also more compact.

## What's the evolution for the future?

**HTTP/3** is under development, and will be adapted from _HTTP-over-QUIC_, an experimental project.

QUIC is a protocol based on UDP (rather than TCP) at the transport layer, which means that HTTP/3 will be based on a completely different tech stack compared to HTTP/2 and HTTP/1.x.