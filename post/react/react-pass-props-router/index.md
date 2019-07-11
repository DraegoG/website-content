---
title: "How to pass props to a child component via React Router"
date: 2017-08-20T11:04:59+02:00
updated: 2018-05-10T11:04:59+02:00
description: "This short tutorial explains how to pass props to a child component via React Router"
tags: react
---

There are many solutions to pass props to a child component via [React Router](/react-router/), and some you'll find are outdated.

The most simple ever is adding the props to the Route wrapper component:

```js
const Index = props => <h1>{props.route.something}</h1>

var routes = <Route path="/" something={'here'} component={Index} />
```

But in this way you need to modify how you access props, via `this.props.route.*` instead than the usual `this.props`, which might or might not be acceptable.

A way to fix this is to use:

```js
const Index = props => (
  <h1>{props.something}</h1>
)

<Route path="/" render={() => <Index something={'here'} />} />
```
