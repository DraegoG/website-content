---
title: The Channel Messaging API
description: The Channel Messaging API allows iframes and workers to communicate with the main document thread, by passing messages
date: 2018-02-07T08:04:59+02:00
updated: 2019-05-11T07:06:29+02:00
tags: browser
---

<!-- TOC -->

- [Introduction to Channel Messaging API](#introduction-to-channel-messaging-api)
  - [How it works](#how-it-works)
- [An example with an iframe](#an-example-with-an-iframe)
- [An example with a Service Worker](#an-example-with-a-service-worker)

<!-- /TOC -->

## Introduction to Channel Messaging API

Given two scripts running in the same document, but in a different context, the Channel Messaging API allows them to communicate by passing messages through a channel.

This use case involves communication between

- the document and an iframe
- two iframes
- two documents

### How it works

Calling `new MessageChannel()` a message channel is initialized.

```js
const channel = new MessageChannel()
```

The channel has 2 properties, called

- port1
- port2

Those properties are a MessagePort object. `port1` is the port used by the part that created the channel, and `port2` is the port used by the channel receiver (by the way, the channel is bidirectional, so the receiver can send back messages as well).

At each end of the channel you listen on one port, and you send messages to the other port.

Sending the message is done through the

```js
otherWindow.postMessage()
```

method, where `otherWindow` is the other browsing context.

It accepts a message, an origin and the port.

For example:

```js
const data = { name: 'Flavio' }
const channel = new MessageChannel()
window.postMessage(data, [channel.port2])
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

"Origin" is a URI (e.g. `https://example.org`). You can use `'*'` to allow less strict checking, or specify a domain, or specify `'/'` to set a same-domain target, without needing to specify which domain is it.

The other browsing context listens for the message using the `message` event:

```js
self.addEventListener('message', event => {
  console.log('A new message arrived!')
})
```

> `self` is same as using `window` in this case

Inside the event handler we can access the data sent by looking at the `data` property of the event object:

```js
self.addEventListener('message', event => {
  console.log('A new message arrived!')
  console.log(event.data)
})
```

We can respond back by using `MessagePort.postMessage`:

```js
self.addEventListener('message', event => {
  console.log('A new message arrived!')
  console.log(event.data)

  const data = { someData: 'hey' }
  event.ports[0].postMessage(data)
})
```

A channel can be closed by invoking the `close()` method on the port:.

```js
self.addEventListener('message', event => {
  console.log('A new message arrived!')
  console.log(event.data)

  const data = { someData: 'hey' }
  event.ports[0].postMessage(data)
  event.ports[0].close()
})
```

## An example with an iframe

Here's an example of a communication happening between a document and an iframe embedded into it.

The main document defines an `iframe` and a `span` where we'll print a message that's sent from the `iframe` document. As soon as the `iframe` document is loaded, we send it a message on the `channel` we created.

```html
<!DOCTYPE html>
<html>
  <body>
    <iframe src="iframe.html" width="500" height="500"></iframe>
    <span></span>
  </body>
  <script>
    const channel = new MessageChannel()
    const display = document.querySelector('span')
    const iframe = document.querySelector('iframe')

    iframe.addEventListener('load', () => {
      iframe.contentWindow.postMessage('Hey', '*', [channel.port2])
    }, false)

    channel.port1.onmessage = event => {
      display.innerHTML = event.data
    }
  </script>
</html>
```

The iframe page source is even simpler:

```html
<!DOCTYPE html>
<html>
  <script>
  window.addEventListener('message', event => {
    // send a message back
    event.ports[0].postMessage('Message back from the iframe')
  }, false)
  </script>
</html>
```

As you can see we don't even need to initialize a channel, because the `window.onmessage` handler is automatically run when the message is received from the container page.

The event sent is composed by the following properties:

- `data`: the object that's been sent from the other window
- `origin`: the origin URI of the window that sent the message
- `source`: the window object that sent the message

Always verify the origin of the message sender.

`e.ports[0]` is the way we reference `port2` in the iframe, because `ports` is an array, and the port was added as the first element.

## An example with a Service Worker

A Service Worker is an event-driven worker, a JavaScript file associated with web page. Check out the [Service Workers guide](/service-workers/) to know more about them.

What's important to know is that Service Workers are isolated from the main thread, and we must communicate with them using messages.

This is how a script attached to the main document will handle sending messages to the Service Worker:

```js
// `worker` is the service worker already instantiated

const messageChannel = new MessageChannel()
messageChannel.port1.addEventListener('message', event => {
  console.log(event.data)
})
worker.postMessage(data, [messageChannel.port2])
```

In the Service Worker code, we add an event listener for the `message` event:

```js
self.addEventListener('message', event => {
  console.log(event.data)
})
```

And it can send messages back by posting a message to `messageChannel.port2`, with

```js
self.addEventListener('message', event => {
  event.ports[0].postMessage(data)
})
```
