---
title: How to use the useRef React hook
date: 2019-07-21T07:00:00+02:00
description: "Find out what the useRef React hook is useful for, and how to work with it!"
tags: react
---

> Check out my [React hooks introduction](/react-hooks/) first, if you're new to them.

One React hook I sometimes use is `useRef`.

```js
import React, { useRef } from 'react'
```

This hook allows us to access a DOM element imperatively.

Here's an example, where I log to the console the value of the DOM reference of the span element that contains the count value:

```js
import React, { useState, useRef } from 'react'

const Counter = () => {
  const [count, setCount] = useState(0)
  const counterEl = useRef(null)

  const increment = () => {
    setCount(count + 1)
    console.log(counterEl)
  }

  return (
    <>
      Count: <span ref={counterEl}>{count}</span>
      <button onClick={increment}>+</button>
    </>
  )
}

ReactDOM.render(<Counter />, document.getElementById('app'))
```

Notice the `const counterEl = useRef(null)` line, and the `<span ref={counterEl}>{count}</span>`. This is what sets the link.

Now we can access the DOM reference by accessing `counterEl.current`.

See it on Codepen:


<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="orENKo" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="React useRef hook">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/orENKo/">
  React useRef hook</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

