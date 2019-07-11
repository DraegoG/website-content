---
title: "Server Side Rendering with React"
date: 2018-12-23T07:00:00+02:00
description: "What is Server Side Rendering? How to do it with React?"
tags: react
---

**Server Side Rendering**, also called **SSR**, is the ability of a JavaScript application to render on the server rather than in the browser.

Why would we ever want to do so?

- it allows your site to have a faster first page load time, which is the key to a good user experience
- it is essential for SEO: search engines cannot (yet?) efficiently and correctly index applications that exclusively render client-side. Despite the latest improvements to indexing in Google, there are other search engines too, and Google is not perfect at it in any case. Also, Google favors sites with fast load times, and having to load client-side is not good for speed
- it's great when people share a page of your site on social media, as they can easily gather the metadata needed to nicely share the link (images, title, description..)

Without Server Side Rendering, all your server ships is an HTML page with no body, just some script tags that are then used by the browser to render the application.

Client-rendered apps are great at any subsequent user interaction after the first page load. Server Side Rendering allows us to get the sweet spot in the middle of client-rendered apps and backend-rendered apps: the page is generated server-side, but all interactions with the page once it's been loaded are handled client-side.

However Server Side Rendering has its drawback too:

- it's fair to say that a simple SSR proof of concept is simple, but the complexity of SSR can grow with the complexity of your application
- rendering a big application server-side can be quite resource-intensive, and under heavy load it could even provide a slower experience than client-side rendering, since you have a single bottleneck

## A very simplistic example of what it takes to Server-Side render a React app

SSR setups can grow very, very complex and most tutorials will bake in Redux, React Router and many other concepts from the start.

To understand how SSR works, let's start from the basics to implement a proof of concept.

> Feel free to skip this paragraph if you just want to look into the libraries that provide SSR and not bother with the ground work

To implement basic SSR we're going to use Express.

> If you are new to Express, or need some catch-up, check out my free Express Handbook here: <https://flaviocopes.com/page/ebooks/>.

Warning: the complexity of SSR can grow with the complexity of your application. This is the bare minimum setup to render a basic React app. For more complex needs you might need to do a bit more work or also check out SSR libraries for React.

I assume you started a React app with `create-react-app`. If you are just trying, install one now using `npx create-react-app ssr`.

Go to the main app folder with the terminal, then run:

```bash
npm install express
```

You have a set of folders in your app directory. Create a new folder called `server`, then go into it and create a file named `server.js`.

Following the `create-react-app` conventions, the app lives in the `src/App.js` file. We're going to load that component, and render it to a string using [ReactDOMServer.renderToString()](https://reactjs.org/docs/react-dom-server.html), which is provided by `react-dom`.

You get the contents of the `./build/index.html` file, and replace the `<div id="root"></div>` placeholder, which is the tag where the application hooks by default, with ``<div id="root">\${ReactDOMServer.renderToString(<App />)}</div>`.

All the content inside the `build` folder is going to be served as-is, statically by Express.

```js
import path from 'path'
import fs from 'fs'

import express from 'express'
import React from 'react'
import ReactDOMServer from 'react-dom/server'

import App from '../src/App'

const PORT = 8080
const app = express()

const router = express.Router()

const serverRenderer = (req, res, next) => {
  fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
    if (err) {
      console.error(err)
      return res.status(500).send('An error occurred')
    }
    return res.send(
      data.replace(
        '<div id="root"></div>',
        `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
      )
    )
  })
}
router.use('^/$', serverRenderer)

router.use(
  express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' })
)

// tell the app to use the above rules
app.use(router)

// app.use(express.static('./build'))
app.listen(PORT, () => {
  console.log(`SSR running on port ${PORT}`)
})
```

Now, in the client application, in your `src/index.js`, instead of calling `ReactDOM.render()`:

```js
ReactDOM.render(<App />, document.getElementById('root'))
```

call [`ReactDOM.hydrate()`](https://reactjs.org/docs/react-dom.html#hydrate), which is the same but has the additional ability to attach event listeners to existing markup once React loads:

```js
ReactDOM.hydrate(<App />, document.getElementById('root'))
```

All the Node.js code needs to be transpiled by [Babel](https://flaviocopes.com/babel/), as server-side Node.js code does not know anything about JSX, nor ES Modules (which we use for the `include` statements).

Install these 3 packages:

```bash
npm install @babel/register @babel/preset-env @babel/preset-react ignore-styles express
```

[`ignore-styles`](https://www.npmjs.com/package/ignore-styles) is a Babel utility that will tell it to ignore CSS files imported using the `import` syntax.

Let's create an entry point in `server/index.js`:

```js
require('ignore-styles')

require('@babel/register')({
  ignore: [/(node_modules)/],
  presets: ['@babel/preset-env', '@babel/preset-react']
})

require('./server')
```

Build the React application, so that the build/ folder is populated:

```bash
npm run build
```

and let's run this:

```bash
node server/index.js
```

I said this is a simplistic approach, and it is:

- it does not handle rendering images correctly when using imports, which need Webpack in order to work (and which complicates the process a lot)
- it does not handle page header metadata, which is essential for SEO and social sharing purposes (among other things)

So while this is a good example of using `ReactDOMServer.renderToString()` and `ReactDOM.hydrate` to get this basic server-side rendering, it's not enough for real world usage.

## Server Side Rendering using libraries

SSR is hard to do right, and React has no de-facto way to implement it.

It's still very much debatable if it's worth the trouble, complication and overhead to get the benefits, rather than using a different technology to serve those pages. [This discussion on Reddit](https://www.reddit.com/r/reactjs/comments/7o6oj6/serverside_rendering_not_worth_it/) has lots of opinions in that regard.

When Server Side Rendering is an important matter, my suggestion is to rely on pre-made libraries and tools that have had this goal in mind since the beginning.

In particular, I suggest **Next.js** and **Gatsby**, two projects we'll see later on.
