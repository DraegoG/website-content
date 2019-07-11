---
title: Conditional rendering in React
date: 2019-01-25T07:00:00+02:00
description: "How to dynamically output something vs something else in React"
tags: react
---

In a React component JSX you can dynamically decide to output some component or another, or just some portion of JSX, based on conditionals.

The most common way is probably the ternary operator:

```js
const Pet = (props) => {
  return (
    {props.isDog ? <Dog /> : <Cat />}
  )
}
```

Another way, which works great when you conceptually have an `if` but not an `else` is to use the `&&` operator, which works this way: if the expression before it evaluates to true, it prints the expression after it:

```js
const Pet = (props) => {
  return (
    {props.isDog && <Dog />}
    {props.isCat && <Cat />}
  )
}
```
