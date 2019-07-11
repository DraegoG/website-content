---
title: How to return multiple elements in JSX
date: 2019-01-24T07:00:00+02:00
description: "How to workaround that the limitation that JSX has when having to return multiple elements from a component"
tags: react
---

When writing JSX in React, there's one caveat: you must return one parent item. Not more than one.

For example, this is not possible:

```js
const Pets = () => {
  return (
    <Dog />
    <Cat />
  )
}
```

One "classic" way to solve this is to wrap components and other HTML elements in a `div`:

```js
const Pets = () => {
  return (
    <div>
      <Dog />
      <Cat />
    </div>
  )
}
```

However this introduces a problem - there's an HTML element that was introduced just to make our JSX work, not necessary in the resulting HTML, but that's where it ends into.

One solution is to to return an array of JSX elements:

```js
const Pets = () => {
  return [
      <Dog />,
      <Cat />
  ]
}
```

Another solution is to use Fragment, a relatively new React feature that solves the problem for us:

```js
const Pets = () => {
  return (
    <Fragment>
      <Dog />
      <Cat />
    </Fragment>
  )
}
```

it works like the `div` element we added before, but it's not going to appear in the resulting HTML rendered to the browser. Win-win.