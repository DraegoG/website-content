---
title: "Introduction to React Hooks"
date: 2018-12-17T07:00:00+02:00
description: "Learn how Hooks can help you build a React application"
tags: react
---

Hooks is a feature that will be introduced in React 16.7, and is going to change how we write React apps in the future.

Before Hooks appeared, some key things in components were only possible using class components: having their own state, and using lifecycle events. Function components, lighter and more flexible, were limited in functionality.

**Hooks allow function components to have state and to respond to lifecycle events** too, and kind of make class components obsolete. They also allow function components to have a good way to handle events.

## Access state

Using the `useState()` API, you can create a new state variable, and have a way to alter it. `useState()` accepts the initial value of the state item and returns an array containing the state variable, and the function you call to alter the state. Since it returns an array we use [array destructuring](https://flaviocopes.com/es6/#destructuring-assignments) to access each individual item, like this: `const [count, setCount] = useState(0)`

Here's a practical example:

```js
import { useState } from 'react'

const Counter = () => {
  const [count, setCount] = useState(0)

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  )
}

ReactDOM.render(<Counter />, document.getElementById('app'))
```

You can add as many `useState()` calls you want, to create as many state variables as you want. Just make sure you call it in the top level of a component (not in an `if` or in any other block).

Example on Codepen:

<p data-height="446" data-theme-id="0" data-slug-hash="maVPKa" data-default-tab="js,result" data-user="flaviocopes" data-pen-title="React Hooks example #1 counter" class="codepen">See the Pen <a href="https://codepen.io/flaviocopes/pen/maVPKa/">React Hooks example #1 counter</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Access lifecycle hooks

Another very important feature of Hooks is allowing function components to have access to the lifecycle hooks.

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

## Enable cross-component communication using custom hooks

The ability to write your own hooks is the feature that is going to significantly alter how you write React apps in the future.

Using custom hooks you have one more way to share state and logic between components, adding a significant improvement to the patterns of render props and higher order components. Which are still great, but now with custom hooks have less relevance in many use cases.

How do you create a custom hook?

A hook is function that conventionally starts with `use`. It can accept an arbitrary number of arguments, and return anything it wants.

Examples:

```js
const useGetData() {
  //...
  return data
}
```

or

```js
const useGetUser(username) {
  //...const user = fetch(...)
  //...const userData = ...
  return [user, userData]
}
```

In your own components, you can use the hook like this:

```js
const MyComponent = () => {
  const data = useGetData()
  const [user, userData] = useGetUser('flavio')
  //...
}
```

When exactly to add hooks instead of regular functions should be determined on a use case basis, and only experience will tell.
