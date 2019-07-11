---
title: Handling redirects with Express
description: "How to redirect to other pages server-side"
date: 2018-09-16T07:00:00+02:00
booktitle: "Express"
tags: express
tags_weight: 5
path: express-redirects
---

Redirects are common in Web Development. You can create a redirect using the `Response.redirect()` method:

```js
res.redirect('/go-there')
```

This creates a 302 redirect.

A 301 redirect is made in this way:

```js
res.redirect(301, '/go-there')
```

You can specify an absolute path (`/go-there`), an absolute url (`https://anothersite.com`), a relative path (`go-there`) or use the `..` to go back one level:

```js
res.redirect('../go-there')
res.redirect('..')
```

You can also redirect back to the Referer HTTP header value (defaulting to `/` if not set) using

```js
res.redirect('back')
```