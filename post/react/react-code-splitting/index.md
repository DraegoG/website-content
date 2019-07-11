---
title: "Code Splitting in React"
date: 2018-12-22T07:00:00+02:00
description: "What is Code Splitting and how to introduce it in a React app"
tags: react
---

Modern JavaScript applications can be quite huge in terms of bundle size. You don't want your users to have to download a 1MB package of JavaScript (your code and the libraries you use) just to load the first page, right? But this is what happens by default when you ship a modern Web App built with Webpack bundling.

That bundle will contain code that might never run because the user only stops on the login page and never sees the rest of your app.

Code splitting is the practice of only loading the JavaScript you need the moment when you need it.

This improves:

- the performance of your app
- the impact on memory, and so battery usage on mobile devices
- the downloaded KiloBytes (or MegaBytes) size

React 16.6.0, released in October 2018, introduced a way of performing code splitting that should take the place of every previously used tool or library: **React.lazy** and **Suspense**.

`React.lazy` and `Suspense` form the perfect way to lazily load a dependency and only load it when needed.

Let's start with `React.lazy`. You use it to import any component:

```js
import React from 'react'

const TodoList = React.lazy(() => import('./TodoList'))

export default () => {
  return (
    <div>
      <TodoList />
    </div>
  )
}
```

the TodoList component will be dynamically added to the output as soon as it's available. Webpack will create a separate bundle for it, and will take care of loading it when necessary.

`Suspense` is a component that you can use to wrap any lazily loaded component:

```js
import React from 'react'

const TodoList = React.lazy(() => import('./TodoList'))

export default () => {
  return (
    <div>
      <React.Suspense>
        <TodoList />
      </React.Suspense>
    </div>
  )
}
```

It takes care of handling the output while the lazy loaded component is fetched and rendered.

Use its `fallback` prop to output some JSX or a component output:

```js
...
      <React.Suspense fallback={<p>Please wait</p>}>
        <TodoList />
      </React.Suspense>
...
```

All this plays well with React Router:

```js
import React from 'react'
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom'

const TodoList = React.lazy(() => import('./routes/TodoList'))
const NewTodo = React.lazy(() => import('./routes/NewTodo'))

const App = () => (
  <Router>
    <React.Suspense fallback={<p>Please wait</p>}>
      <Switch>
        <Route exact path="/" component={TodoList} />
        <Route path="/new" component={NewTodo} />
      </Switch>
    </React.Suspense>
  </Router>
)
```
