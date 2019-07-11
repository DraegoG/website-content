---
title: "ArrayBuffer"
date: 2019-05-12T07:00:00+02:00
description: "Find out what is an ArrayBuffer and how to use it"
tags: browser
---

Just as a [Blob](/blob/) is an opaque representation of data available on disk, an **ArrayBuffer** is an opaque representation of bytes available in memory.

The constructor takes one parameter, the length in bytes:

```js
const buffer = new ArrayBuffer(64)
```

An ArrayBuffer value has one (read-only) property: `byteLength`, which - as the name suggests - expresses its length in bytes.

It also provides a `slice()` instance method which creates a new `ArrayBuffer` from an existing one, taking a starting position and an optional length:

```js
const buffer = new ArrayBuffer(64)
const newBuffer = buffer.slice(32, 8)
```

## Downloading data from the internet as an ArrayBuffer

We can download a blob from the internet and store it into an ArrayBuffer using [XHR](/xhr/):

```js
const downloadBlob = (url, callback) => {
	const xhr = new XMLHttpRequest()
	xhr.open('GET', url)
	xhr.responseType = 'arraybuffer'

	xhr.onload = () => {
    callback(xhr.response)
	}

	xhr.send(null)
}
```
