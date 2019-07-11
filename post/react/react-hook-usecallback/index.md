---
title: How to use the useCallback React hook
date: 2019-07-18T07:00:00+02:00
description: "Find out what the useCallback React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I sometimes use is `useCallback`.

```js
import React, { useCallback } from 'react'
```

This hook is useful when you have a component with a child frequently re-rendering, and you pass a callback to it:

```js
import React, { useState, useCallback } from 'react'

const Counter = () => {
  const [count, setCount] = useState(0)
  const [otherCounter, setOtherCounter] = useState(0)

  const increment = () => {
    setCount(count + 1)
  }
  const decrement = () => {
    setCount(count - 1)
  }
  const incrementOtherCounter = () => {
    setOtherCounter(otherCounter + 1)
  }

  return (
    <>
      Count: {count}
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={incrementOtherCounter}>incrementOtherCounter</button>
    </>
  )
}

ReactDOM.render(<Counter />, document.getElementById('app'))
```

The problem here is that any time the counter is updated, all the 3 functions are re-created again.

You can visualize this by instantiating a [Set data structure](/javascript-data-structures-set/), and adding each function to it. Why Set? because it only stores unique elements, which in our case means different (uniquely instantiated) functions.

```js
import React, { useState, useCallback } from 'react'

const functionsCounter = new Set()

const Counter = () => {
  const [count, setCount] = useState(0)
  const [otherCounter, setOtherCounter] = useState(0)

  const increment = () => {
    setCount(count + 1)
  }
  const decrement = () => {
    setCount(count - 1)
  }
  const incrementOtherCounter = () => {
    setOtherCounter(otherCounter + 1)
  }

  functionsCounter.add(increment)
  functionsCounter.add(decrement)
  functionsCounter.add(incrementOtherCounter)

  alert(functionsCounter)

  return (
    <>
      Count: {count}
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={incrementOtherCounter}>incrementOtherCounter</button>
    </>
  )
}

ReactDOM.render(<Counter />, document.getElementById('app'))
```

If you try out this code you'll see the alert incrementing by 3 at a time.

What should happen instead it's that if you increment one counter, all functions related to that counter should be re-instantiated.

If another state value is unchanged, it should not be touched.

Now, in most cases this is not a huge problem unless you are passing lots of different functions, all changing unrelated bits of data, that are proven to be a big cost for your app performance.

If that's a problem, you can use `useCallback`.

This is how we do it. Instead of:

```js
const increment = (() => {
  setCount(count + 1)
})
const decrement = (() => {
  setCount(count - 1)
})
const incrementOtherCounter = (() => {
  setOtherCounter(otherCounter + 1)
})
```

You wrap all those calls in:

```js
const increment = useCallback(() => {
  setCount(count + 1)
}, [count])
const decrement = useCallback(() => {
  setCount(count - 1)
}, [count])
const incrementOtherCounter = useCallback(() => {
  setOtherCounter(otherCounter + 1)
}, [otherCounter])
```

Make sure you add that array as a second parameter to `useCallback()` with the state needed.

Now if you try to click one of the counters, only the functions related to the state that changes are going to be re-instantiated.

You can try this example on Codepen:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="VJQwzb" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="React useCallback hook">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/VJQwzb/">
  React useCallback hook</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

