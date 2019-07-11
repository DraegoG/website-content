---
title: "Run a web server from any folder"
date: 2018-11-13T07:00:00+02:00
description: ""
tags: node
---

A common need you can have is to spin up a Web Server from a particular folder in your system.

You have absolutely no time to configure a proper web server like Apache or Nginx because this is just for a few minutes or for testing your app.

How do you do so?

Depending on the language you prefer, you might already have all you need.

If you use [Node.js](/nodejs/) and you have installed [`npm`](/npm/) already, run

```bash
npm install -g http-server
```

and then run `http-server` in the folder you want to expose through your server.

By default it will start the server on port 8080, but you can change it using the `-p` flag (see more options by running `http-server --help`).

If you use Python and have it installed, just run

```bash
python -m SimpleHTTPServer 8080
```

(Python 2)

or

```bash
python -m http.server 8080
```

(Python 3)

to start a local server on port 8080.

If you use PHP and you run a modern version of it, run

```bash
php -S localhost:8080
```
