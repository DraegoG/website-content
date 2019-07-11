---
title: How to encode a URL with JavaScript
description: "You might need to encode a URL if you are sending it as part of a GET request, for example."
date: 2018-12-04T07:00:00+02:00
tags: js
---

How do you encode a URL in JavaScript?

Depending on what you need to do, there are 2 JavaScript functions what will help you.

The first is `encodeURI()`, and the second is `encodeURIComponent()`.

> Note: you might read about `escape()`, but that is deprecated and should not be used.

Those 2 methods differ in which characters they do encode.

In details, `encodeURI()` does not encode `~!@#$&*()=:/,;?+` and `encodeURIComponent()` does not encode `-_.!~*'()`, encoding all the other characters. Why do they differ? Because they are meant for different uses:

- `encodeURI()` is meant to encode a full URL
- `encodeURIComponent()` is meant to encode a single URL parameter value

If you were to call `encodeURIComponent()` on a full URL, since it does encode `/`, the URL path separators would be encoded as well (among other things):

```js
encodeURI("http://flaviocopes.com/ hey!/")
//"http://flaviocopes.com/%20hey!/"
encodeURIComponent("http://www.example.org/a file with spaces.html")
// "http%3A%2F%2Fflaviocopes.com%2F%20hey!%2F"
```

[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) proposes an improvement to adhere to the [RFC](/rfc/) 3986 standard (<http://tools.ietf.org/html/rfc3986>), by implementing the following function:

```js
const fixedEncodeURIComponent = (str) => {
  return encodeURIComponent(str).replace(/[!'()*]/g, (c) => {
    return '%' + c.charCodeAt(0).toString(16)
  })
}
```

You call it for every single parameter that you'll add to the URL.

The `encodeURI()` and `encodeURIComponent()` methods have a corresponding `decodeURI()` and `decodeURIComponent()` which does the opposite job which you can use on the backend if you use [Node.js](/nodejs/).
