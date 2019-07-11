---
title: "Introduction to PeerJS, the WebRTC library"
date: 2019-01-02T07:00:00+02:00
description: "Working with WebRTC can be hard. PeerJS is an awesome library that makes WebRTC easier"
---

I wrote about [WebRTC](/webrtc/). That post described the details of working with the protocol to make 2 Web browsers communicate with each other directly.

In that tutorial I mentioned that there are libraries that abstract the many details you have to take care to allow WebRTC communication.

One of those libraries is PeerJS, which makes real time communication extremely simple.

First thing is, you need to have a backend to allow 2 clients to synchronize before they are able to directly talk to each other.

In a folder, initialize an [npm](/npm/) project using `npm init`, install PeerJS using `npm install peerjs` and then and you can run it using [`npx`](/npx/):

```bash
npx peerjs --port 9000
```

(run `npx peerjs --help` to see all the options you can use).

This is your backend 🙂

Now we can create the simplest application that does anything useful. We have one receiver and one sender.

First we create the receiver, which connects to our PeerJS server, and listens for data coming in to it. The first parameter to `new Peer()` is our peer name, which we call `receiver` to make it clear:

Include the PeerJS client (change the library version with the latest available):

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/peerjs/0.3.16/peer.min.js"></script>
```

Then we initialize the `Peer` object. The `connection` event is called when another peer connects to us. When we receive some data, the `data` event is called with the payload:

```js
const peer = new Peer('receiver', { host: 'localhost', port: 9000, path: '/' })

peer.on('connection', (conn) => {
  conn.on('data', (data) => {
    console.log(data);
  })
})
```

Let's create the other end of the communication. We'll call this `sender` because it's the one that will connect and send a message to the receiver.

We initialize the `Peer` object, then we ask the peer to connect to the `receiver` peer, which we registered earlier. Then once the connection is established the `open` event fires, and we can call the `send()` method on the connection to send data to the other end:

```js
const peer = new Peer('sender', { host: 'localhost', port: 9000, path: '/' })

const conn = peer.connect('receiver')

conn.on('open', () => {
  conn.send('hi!')
})
```

That is the most basic example you can make.

First you open the receiver page, then you open the sender page. The receiver gets the message *directly* from the sender, not from a centralized resource. The server part is only needed to exchange information so the 2 parts can connect. After that, it's not interfering any more.