---
title: "The Reach Router Tutorial"
date: 2019-07-27T07:00:00+02:00
description: "A quickstart to using Reach Router in your React app"
tags: react
---

In the last project I did I used [Reach Router](https://reach.tech/router/) and I think it's the simplest way to have routing in a React app.

I think it's much easier than [React Router](/react-router/), which is another router I used in the past.

Here's a 5 minutes tutorial to get the basics of it.

## Installation

First, install it using

```sh
npm install @reach/router
```

> If the `@` syntax is new to you, it's an npm feature to allow a scoped package. A namespace, in other words.

Next, import it in your project.

```js
import { Router } from '@reach/router'
```

## Basic usage

I use it in the top-level React file, `index.js` in a [create-react-app](/react-create-react-app/) installation, wrapping all components that I want to appear:

```jsx
ReactDOM.render(
  <Router>
    <Form path="/" />
    <PrivateArea path="/private-area" />
  </Router>,
  document.getElementById('root')
)
```

The `path` attribute I add to the components allows me to set the path for them.

In other words, when I type that path in the browser URL bar, Reach Router shows that specific component to me.

The `/` path is the index route, and shows up when you don't set a URL / path beside the app domain. The "home page", in other words.

## The default route

When a user visits an URL that does not match any route, by default Reach Router redirects to the `/` route. You can add a `default` route to handle this case and display a nice "404" message instead:

```jsx
<Router>
  <Form path="/" />
  <PrivateArea path="/private-area" />
  <NotFound default />
</Router>
```

## Programmatically change the route

Use the `navigate` function to programmatically change the route in your app:

```js
import { navigate } from '@reach/router'
```

```js
navigate('/private-area')
```

## Link to routes in JSX

Use the `Link` component to link to your routes using JSX:

```js
import { navigate } from '@reach/router'
```

```jsx
<Link to="/">Home</Link>
<Link to="/private-area">Private Area</Link>
```

## URL parameters

Add parameters using the `:param` syntax:

```jsx
<Router>
  <User path="users/:userId" />
</Router>
```

Now in this hypothetical User component we can get the `userId` as a prop:

```js
const User = ({ userId }) => (
  <p>User {userId}</p>
)
```

## Nested routes

I showed you how routes can be defined in this way in your top level React file:

```jsx
<Router>
  <Form path="/" />
  <PrivateArea path="/private-area" />
</Router>
```

You can define nested routes:

```jsx
<Router>
  <Form path="/" />
  <PrivateArea path="/private-area">
    <User path=":userId" />
  </PrivateArea>
</Router>
```

So now you can have your `/private-area/23232` link point to User component, passing the `userId` `23232`.

You can also choose to allow a component to define its own routes inside it. You use the `/*` wildcard after the route:

```jsx
<Router>
  <Form path="/" />
  <PrivateArea path="/private-area/*" />
</Router>
```

then inside the component you can import Router again, and define its own set of sub-routes:

```jsx
//component PrivateArea
<Router>
  <User path="/:userId" />
</router>
```

Any route using `/private-area/something` will be handled by the User component, and the part after the route will be sent as its `userId` prop.

To display something in the `/private-area` route now you also need to add a `/` handler in the `PrivateArea` component:

```jsx
//component PrivateArea
<Router>
  <User path="/:userId" />
  <PrivateAreaDashboard path="/" />
</router>
```