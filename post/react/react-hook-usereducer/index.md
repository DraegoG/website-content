---
title: How to use the useReducer React hook
date: 2019-07-17T07:00:00+02:00
description: "Find out what the useReducer React hook is useful for, and how to work with it!"
tags: react
---

Since React introduced **hooks**, I worked with them on several projects and they are just great.

Removing all class-based components makes the code feel much more "real" JavaScript. And functional components can finally manage state.

Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One hook I sometimes use is `useReducer`.

```js
import React, { useReducer } from 'react'
```

This hook is used to manage state. Sort of like `useState`, except more complex.

This is the key difference between `useState` and `useReducer`: with `useReducer`, **state is altered by passing messages** rather than calling the updater function.

If you know how [Redux](/redux/) works, that's basically the same. A reducer is a pure function that calculates the next state based on the previous state and the action that has been dispatched.

```js
(currentState, action) => newState
```

What does "pure function" mean? A pure function takes an input and returns an output without changing the input or anything else. This means that a reducer returns a completely new state that substitutes the previous one.

A reducer should:

- never mutate its arguments
- never generate side-effects (no API calls changing anything)
- never call non-pure functions, functions that change their output based on factors other than their input (e.g. `Date.now()` or `Math.random()`)

There is no reinforcement, but you should stick to the rules. And this has a nice benefit: reducers are much simpler to test, because they have no side effects.

This allows to centralize the state management, allowing components to modify it by sending messages, and also allows you to use (and alter) a more complex state in your components.

Let's do an example, with a counter component.

`useReducer` accepts as arguments a reducer function, and an initial state value. In this case our state is an integer, which starts from 0:

```js
const Counter = () => {
  const [state, dispatch] = useReducer(reducer, 0)
}
```

The reducer is a function that takes, as explained above, the current state and an action, which can be a value of any type you want. In this case it's a string:

```js
const reducer = (state, action) => {
  switch (action) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      throw new Error()
  }
}
```

We also make the component output some [JSX](/jsx/) to make this simple app work:

```js
const Counter = () => {
  const [count, dispatch] = useReducer(reducer, 0)
  return (
    <>
      Counter: {count}
      <button onClick={() => dispatch('INCREMENT')}>+</button>
      <button onClick={() => dispatch('DECREMENT')}>-</button>
    </>
  )
}
```

Here is the full example on Codepen:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="MMQgrB" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="React useReducer hook">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/MMQgrB/">
  React useReducer hook</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

Now, imagine this state can be an object with many many properties, and different actions only change one property at a time. That's a great use case for this hook.
