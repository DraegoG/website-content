---
title: "How to only accept images in an input file field"
date: 2018-12-18T07:00:00+02:00
description: "When adding a file field to a form, you might want to limit the selector to images"
tags: browser
---

Of course you could add a server-side filter, but also having a client-side filter is a great UX for your users - no time wasted and no resources wasted to send a file to you and get back with an error.

You can do so by using the `accept` attribute, and specifying the MIME type of the files you accept.

`image/*` should catch all images.

```html
<input type="file" name="myImage" accept="image/*" />
```

If you want to only allow some specific file types, list them:

```html
<input type="file" name="myImage" accept="image/x-png,image/gif,image/jpeg" />
```

You can check the browser support for this attribute here: <https://caniuse.com/#feat=input-file-accept>