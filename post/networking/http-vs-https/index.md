---
title: HTTP vs HTTPS
description: Explore the main differences between HTTP and HTTPS, see why HTTPS is faster and better for everything
date: 2018-07-30T07:07:09+02:00
tags: network
---

HTTP (_Hyper Text Transfer Protocol_) is the protocol that powers the web as we know it.

It sits on top of TCP, which sits on top of IP.

Web pages can either use HTTP or HTTPS (_Hyper Text Transfer Protocol Secure_).

How are they different? And, why is now HTTP being marked as non-secure by Chrome?

## Security

When you request an HTTP page from a server, the data goes through many different networks, each controlled by a separate company or entity.

Starting from the WiFi router, which might be owned by the coffee shop or by the city public network infrastructure, every single node in the network can see the request and the response, and modify it in any way.

They might inject ads, they might inject malware, they might log any credentials you enter. A server in the middle can play as a man-in-the-middle, sending compromised information.

This also applies to any internet protocol that's not secured.

HTTPS traffic is end-to-end encrypted, and this means there is nothing in between that can read the information exchanged between you and the server at the other side of the network.

## The ports

By default, HTTP is served on port 80, while HTTPS is served on port 443. Those are the default ports, but a web server can choose to serve content on a different, random port, in which case you need to specify it in the address bar:

```txt
http://flaviocopes.com
http://flaviocopes.com:80/javascript
https://flaviocopes.com:8081/javascript
```

## Is HTTPS slower?

No! It's the opposite.

There is a myth around page speed. People think that the TLS handshake required for HTTPS is making page speed slower, but in reality, an HTTPS page can load up way, **way faster than HTTP**.

Why? Because of [HTTP/2](/http-2/), the newest version of the HTTP protocol.
HTTP/2 can serve requests in parallel, and *requires* a secure connection, so if your server uses a modern Web Server, which supports HTTP/2, then your web pages are going to have a significant speed bump when using HTTPS.

HTTP/2 introduces better parallelism, multiplexing, and compression, and that is an awesome update to HTTP.

See this page for an example: <[https://www.httpvshttps.com/\>](https://www.httpvshttps.com/) and <[https://www.troyhunt.com/i-wanna-go-fast-https-massive-speed-advantage/\>](https://www.troyhunt.com/i-wanna-go-fast-https-massive-speed-advantage/)

## Does HTTPS affect SEO?

Yes.

In particular, [Google says](http://searchengineland.com/google-starts-giving-ranking-boost-secure-httpsssl-sites-199446) HTTPS is going to give you an advantage in SEO terms.

Also, Google is going to officially mark HTTP sites as non-secure in its Chrome browser, and this is clearly an indication that if you care what Google wants, and you want to take advantage of that, you should switch to HTTPS, as soon as possible. The best possible time would have been 3 years ago, the next best time is today.

## Is HTTPS difficult to implement?

Not at all. Thanks to free SSL certificates provided by Let's Encrypt, the push for HTTPS had a huge impact and how every decent hosting provider is implementing it for free on all the accounts. Thanks to this, in 2018 [HTTPS connections were more than the HTTP connections](https://security.googleblog.com/2018/02/a-secure-web-is-here-to-stay.html).

In the past having an SSL certificate for your site was a premium option that few were willing to purchase for a regular site, that was not making money or didn't process user data.

Nowadays there's no excuse.