---
title: "The DataView Object"
date: 2019-05-17T07:00:00+02:00
description: "Find out what is a DataView object and how to use it"
tags: browser
---

`DataView` is a view into an [**ArrayBuffer**](/arraybuffer/), like [Typed Arrays](/typed-arrays/), but in this case the items in the array can have different sizes and types.

Here's an example:

```js
const buffer = new ArrayBuffer(64)
const view = new DataView(buffer)
```

Since this is a view over a buffer, we can specify which byte we want to start from, and the length:

```js
const view = new DataView(buffer, 10) //start at byte 10
```

```js
const view = new DataView(buffer, 10, 30) //start at byte 10, and add 30 items
```

If we don't add those additional arguments, the view starts at position 0 and loads all the bytes present in the buffer.

There is a set of methods we can use to add data into the buffer:

- `setInt8()`
- `setInt16()`
- `setInt32()`
- `setUint8()`
- `setUint16()`
- `setUint32()`
- `setFloat32()`
- `setFloat64()`

This is how to call one of those methods:

```js
const buffer = new ArrayBuffer(64)
const view = new DataView(buffer)
view.setInt16(0, 2019)
```

By default data is stored using **big endian** notation. You can overwrite this setting and use little endian by adding a third parameter with the `true` value:

```js
const buffer = new ArrayBuffer(64)
const view = new DataView(buffer)
view.setInt16(0, 2019, true)
```

Here is how we can get data from the view:

- `getInt8()`
- `getInt16()`
- `getInt32()`
- `getUint8()`
- `getUint16()`
- `getUint32()`
- `getFloat32()`
- `getFloat64()`

Example:

```js
const buffer = new ArrayBuffer(64)
const view = new DataView(buffer)
view.setInt16(0, 2019)
view.getInt16(0) //2019
```

Since a `DataView` is an `ArrayBufferView`, we have those 3 read-only properties:

- `buffer` points to the original ArrayBuffer
- `byteOffset` is the offset on that buffer
- `byteLength` is the length of its content in bytes

One thing to keep in mind is that typed arrays don't let us control the endianness: **it uses the endianness of the system**. In general this works out fine, because the main use case as we said is to use the array locally, using one of the multimedia APIs.

If you transfer the data of a Typed Array on another system, the data might be not badly encoded if it uses Big Endian and you use Little Endian.

In case you need this kind of control, **DataView** is a perfect choice.

