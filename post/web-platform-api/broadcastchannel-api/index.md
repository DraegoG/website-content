---
title: "The BroadcastChannel API"
description: "Learn the basics of 1-to-many communication using the BroadcastChannel API"
date: 2019-05-23T07:00:00+02:00
tags: browser
---

The Channel Messaging API is a great way to send 1-to-1 messages from a window to an iframe, from a window to a Web Worker, and so on.

The BroadcastChannel API can be used to send 1-to-many messages, communicating to multiple entities at the same time.


<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/692rrEwBZvc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>


You start by initializing a `BroadcastChannel` object:

```js
const channel = new BroadcastChannel('thechannel')
```

To send a message on the channel you use the `postMessage()` method:

```js
channel.postMessage('Hey!')
```

A message can be any of those supported values:

- All primitive types, excluding symbols
- [Arrays](/javascript-array/)
- Object literals
- [String](/javascript-string/), [Date](/javascript-dates/), [RegExp](/javascript-regular-expressions/) objects
- [Blob](/blob/), [`File`](/file/), [`FileList`](/filelist/) objects
- [`ArrayBuffer`](/arraybuffer/), [`ArrayBufferView`](/arraybufferview/) objects
- [FormData](/formdata/) objects
- ImageData objects
- [Map](/javascript-data-structures-map/) and [Set](/javascript-data-structures-set/) objects

To receive messages from the channel, listen to the `message` event:

```js
channel.onmessage = event => {
  console.log('Received', event.data)
}
```

This event is fired for all listeners, except the one that is sending the message.

You can close the channel using:

```js
channel.close()
```
