---
title: "React StrictMode"
date: 2018-12-30T07:00:00+02:00
description: "What is React StrictMode and how to use it"
tags: react
---

You can use the `React.StrictMode` built-in component to enable a set of checks that React performs and warns you about.

An easy way is to wrap the entire App component in `<React.StrictMode></React.StrictMode>` in the index.js file:

```js
import React from 'react'
import ReactDOM from 'react-dom'

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
document.getElementById('root')
```

You can also use it by wrapping one or more components of your app:

```js
import React from 'react'

class Hello extends React.Component {
  render() {
    return (
    <div>
      <React.StrictMode>
      ...
      </React.StrictMode>
    <div>
    )
  }
}
```

One of the main use cases of this component is to be used as an automated best practices, potential problems and deprecations check.

It can't catch all, but you have lots of nice checks here that can help you fix the low-hanging fruits.

Introduced in React 16.3 in March 2018, it has zero impact in production, so you can always leave the component in the codebase. Used in development it will print useful warnings in the browser JavaScript console.