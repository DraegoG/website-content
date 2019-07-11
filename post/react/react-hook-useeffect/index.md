---
title: How to use the useEffect React hook
date: 2019-07-19T07:00:00+02:00
description: "Find out what the useEffect React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I sometimes use is `useEffect`.

```js
import React, { useEffect } from 'react'
```

One very important feature of Hooks is allowing function components to have access to the lifecycle hooks.

Using class components you can register a function on the `componentDidMount`, `componentWillUnmount` and `componentDidUpdate` events, and those will serve many use cases, from variables initialization to API calls to cleanup.

Hooks provide the `useEffect()` API. The call accepts a function as argument.

The function runs when the component is first rendered, and on every subsequent re-render/update. React first updates the DOM, then calls any function passed to `useEffect()`. All without blocking the UI rendering even on blocking code, unlike the old `componentDidMount` and `componentDidUpdate`, which makes our apps feel faster.

Example:

```js
const { useEffect, useState } = React

const CounterWithNameAndSideEffect = () => {
  const [count, setCount] = useState(0)
  const [name, setName] = useState('Flavio')

  useEffect(() => {
    console.log(`Hi ${name} you clicked ${count} times`)
  })

  return (
    <div>
      <p>
        Hi {name} you clicked {count} times
      </p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
      <button onClick={() => setName(name === 'Flavio' ? 'Roger' : 'Flavio')}>
        Change name
      </button>
    </div>
  )
}

ReactDOM.render(
  <CounterWithNameAndSideEffect />,
  document.getElementById('app')
)
```

The same `componentWillUnmount` job can be achieved by optionally **returning** a function from our `useEffect()` parameter:

```js
useEffect(() => {
  console.log(`Hi ${name} you clicked ${count} times`)
  return () => {
    console.log(`Unmounted`)
  }
})
```

`useEffect()` can be called multiple times, which is nice to separate unrelated logic (something that plagues the class component lifecycle events).

Since the `useEffect()` functions are run on every subsequent re-render/update, we can tell React to skip a run, for performance purposes, by adding a second parameter which is an array that contains a list of state variables to watch for.
React will only re-run the side effect if one of the items in this array changes.

```js
useEffect(
  () => {
    console.log(`Hi ${name} you clicked ${count} times`)
  },
  [name, count]
)
```

Similarly you can tell React to only execute the side effect once (at mount time), by passing an empty array:

```js
useEffect(() => {
  console.log(`Component mounted`)
}, [])
```

`useEffect()` is great for adding logs, accessing 3rd party APIs and much more.

Example on Codepen:

<p data-height="627" data-theme-id="0" data-slug-hash="WLrxXp" data-default-tab="js,result" data-user="flaviocopes" data-pen-title="React Hooks example #3 side effects" class="codepen">See the Pen <a href="https://codepen.io/flaviocopes/pen/WLrxXp/">React Hooks example #3 side effects</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>