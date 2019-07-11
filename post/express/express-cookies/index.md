---
title: Manage Cookies with Express
description: "How to use the `Response.cookie()` method to manipulate your cookies"
date: 2018-09-23T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-cookies
---

Use the `Response.cookie()` method to manipulate your cookies.

Examples:

```js
res.cookie('username', 'Flavio')
```

This method accepts a third parameter which contains various options:

```js
res.cookie('username', 'Flavio', { domain: '.flaviocopes.com', path: '/administrator', secure: true })

res.cookie('username', 'Flavio', { expires: new Date(Date.now() + 900000), httpOnly: true })
```

The most useful parameters you can set are:

Value | Description
---------|----------
`domain` | 	the [cookie domain name](/cookies/#set-a-cookie-domain)
`expires` | set the [cookie expiration date](/cookies/#set-a-cookie-expiration-date). If missing, or 0, the cookie is a session cookie
`httpOnly` | 	set the cookie to be accessible only by the web server. See [HttpOnly](/cookies/#httponly)
`maxAge` | 	set the expiry time relative to the current time, expressed in milliseconds
`path` | 	the [cookie path](/cookies/#set-a-cookie-path). Defaults to /
`secure` | 	Marks the [cookie HTTPS only](/cookies/#secure)
`signed` | 	set the cookie to be signed
`sameSite` | Value of [`SameSite`](/cookies/#samesite)

A cookie can be cleared with

```js
res.clearCookie('username')
```
