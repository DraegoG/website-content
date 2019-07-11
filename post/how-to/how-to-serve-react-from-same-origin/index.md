---
title: How to connect your React app to a backend on the same origin
date: 2019-07-18T07:00:00+02:00
description: "How to serve a React and a server-side backend app from the same origin, without having to use CORS on the server and worrying about ports"
tags: react
---

I think the single most used way to start a React app is using `create-react-app`. It's very convenient.

One problem you might stumble upon is how to connect it to a backend you already have, or one you might want to create.

## In development

When developing the app you want to take advantage of hot reloading and all the other convenient features of create-react-app. How can you combine that with a backend without having to use CORS on the server and worry about ports?

I am going to provide an example using Express in the post, but this applies to any other framework.

Assuming you are testing this, let's create a React app:

```bash
npx create-react-app testing
```

then

```bash
cd testing
```

Now create a simple Express server in a server.js file, which you can add anywhere you want. It can even be in a separate folder altogether.

If you choose to add this file inside the `create-react-app` application code, run:

```bash
npm install express
```

And we're ready to go.
Add this simple Express setup:

```js
const express = require('express');
const app = express();

app.get('/hey', (req, res) => res.send('ho!'))

app.listen(8080)
```

Crucial point here: open the `package.json` file and add this line somewhere:

```json
"proxy": "http://localhost:8080"
```

This tells React to proxy API requests to the Node.js server built with Express.

Now run this Node process using `node server.js`. In another window you start the CRA app using `npm start`.

When the browser opens on port 3000 (by default), open the DevTools and run:

```js
fetch('/hey')
```

If you check the network panel, you should have a successful response with the `ho!` message.

## In production

In production, you are going to run `npm run build` when you are ready to deploy and we will use the Express server to serve those static files.

The whole proxy thing is now useless (and will not work in production, too - it's meant to ease development). Which means you can leave it in the `package.json` file if you find it convenient.

In the code below, we require the `path` built-in Node module and we tell the app to serve the static build of the React app:

```js
const express = require('express')
const path = require('path')
const app = express()

app.use(express.static(path.join(__dirname, 'build')))

app.get('/ping', (req, res) => {
  return res.send('pong')
})

app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'build', 'index.html'))
})

app.listen(8080)
```
