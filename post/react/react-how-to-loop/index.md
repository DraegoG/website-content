---
title: "How to loop inside React JSX"
date: 2018-11-06T07:00:00+02:00
description: "How to loop in a React component JSX"
tags: react
---

If you have a set of elements you need to loop upon to generate a JSX partial, you can create a loop, and then add JSX to an array:

```js
const elements = [] //..some array

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<Element key={index} />)
}
```

Now when rendering the JSX you can embed the `items` array by wrapping it in curly braces:

```js
render() {
  const elements = ['one', 'two', 'three'];

  const items = []

  for (const [index, value] of elements.entries()) {
    items.push(<li key={index}>{value}</li>)
  }

  return (
    <div>
      {items}
    </div>
  )
}
```

You can do the same directly in the JSX, using `map` instead of a for-of loop:

```js
render: function() {
  const elements = ['one', 'two', 'three'];
  return (
    <ul>
      {elements.map((value, index) => {
        return <li key={index}>{value}</li>
      })}
    </ul>
  )
}
```