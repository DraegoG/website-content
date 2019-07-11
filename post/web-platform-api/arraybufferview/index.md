---
title: "ArrayBufferView"
date: 2019-05-12T15:00:00+02:00
description: "Find out what is an ArrayBufferView object and how to use it"
tags: browser
---

An **ArrayBufferView** is a portion of an [ArrayBuffer](/arraybuffer/).

It has an offset, and a length.

Once created, it provides 3 read-only properties:

- `buffer` points to the original ArrayBuffer
- `byteOffset` is the offset on that buffer
- `byteLength` is the length of its content in bytes

**Typed Arrays** and **DataView**s are instances of an ArrayBufferView.