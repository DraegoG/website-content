---
title: "The Navigator Object"
date: 2019-07-16T07:00:00+02:00
description: "Find out what is the Navigator object and how to use it"
tags: browser
---

The `window.navigator` property exposed by browsers points to a **Navigator object** which is a _container object_ that makes a lot of Web Platform APIs available to us.

The standard and widely implemented properties include:

- `cookieEnabled` true if [cookies](/cookies/) are enabled
- `geolocation` points to the `Geolocation` object used by the **Geolocation API**
- `language` returns a string representing the language currently active in the browser
- `onLine` returns true if the browser is online (the browsers interpret this in different ways, be aware)
- `serviceWorker` the `ServiceWorkerContainer` object assigned to the document (see [Service Workers](/service-workers/))
- `userAgent` the name of the User Agent identifier of the browser

The standard methods include:

- `registerProtocolHander()` a way to let websites register as handlers for protocols.

There are many more methods and properties which are provided by APIs that are either experimental or implemented as drafts and not yet finalized, or just available on a tiny fraction of browsers, so I haven't included them here but [you can explore them all on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator).