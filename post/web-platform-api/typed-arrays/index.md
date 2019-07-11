---
title: "Typed Arrays"
date: 2019-05-16T07:00:00+02:00
description: "Find out what Typed Arrays are and how to use them"
tags: browser
---

JavaScript Provides 8 **Typed Array** types:

- `Int8Array` an array of 8-bit signed integers
- `Int16Array` an array of 16-bit signed integers
- `Int32Array` an array of 32-bit signed integers
- `Uint8Array` an array of 8-bit unsigned integers
- `Uint16Array` an array of 16-bit unsigned integers
- `Uint32Array` an array of 32-bit unsigned integers
- `Float32Array` an array of 32-bit floating point numbers
- `Float64Array` an array of 64-bit floating point numbers

all of them are [`ArrayBufferView`](/arraybufferview/) instances.

A Typed Array is essentially a view into an [`ArrayBuffer`](/arraybuffer/), where every item has the same size, and type.

> `DataView` is another view into an ArrayBuffer, but in this case the items in the array can have different sizes and types.

Here's an example of how to create an array of 8-bit signed integers:

```js
const a = new Int8Array()
```

You can pre-allocate n bytes:

```js
const bytes = 1024
const a = new Int8Array(bytes)
```

The main use is to allow to look into an ArrayBuffer, which on its own is opaque (we can't inspect its content).

Here's how we do so:

```js
//we got this `buffer` ArrayBuffer
const a = new Int8Array(buffer)
```

Those typed arrays are array-like, so now we can inspect the content of the buffer via the usual array access techniques, and we have access to lots of methods and properties including `map()`, `reduce()` and so on.

The main use case for Typed Arrays is to use with **WebGL**, **Web Audio** or the [**Canvas API**](/canvas/). Some of the WebGL functions are expecting typed arrays, as they are much more performant than regular JavaScript arrays.

One thing to keep in mind is that typed arrays don't let us control the *endianness*: **it uses the byte order of the platform**. In general this works out fine, because the main use case as we said is to use the array locally, using one of the multimedia APIs. Also, most consumer computers use little endian since Intel uses that convention. But, if you transfer the data of a Typed Array on a system that uses big endian, the data might be badly encoded and, as such, invalid.

In case you need this kind of control over endianness, use **DataView** instead.