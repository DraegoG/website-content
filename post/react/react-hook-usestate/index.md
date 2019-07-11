---
title: How to use the useState React hook
date: 2019-07-15T07:00:00+02:00
description: "Find out what the useState React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I most often use is `useState`.

```js
import React, { useState } from 'react'
```

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
