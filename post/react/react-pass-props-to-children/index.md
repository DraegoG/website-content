---
title: React, how to transfer props to child components
date: 2019-01-26T07:00:00+02:00
description: "How to pass all props a components gets from its parent, to its own children, in React"
tags: react
---

Suppose you have a hierarchy of components, where you pass props from a top component, and you need to pass those props unaltered to a children. It happens many times, and you don't really want to do like this:

```js
const IntermediateComponent = (props) => {
  return (
    <ChildComponent prop1={props.prop1} prop2={props.prop2} />
  )
}
```

instead, you want to pass all the props, regardless of their name.

You can do so with the [spread operator](/javascript-spread-operator/):

```js
const IntermediateComponent = (props) => {
  return (
    <ChildComponent {...props} />
  )
}
```

This syntax is much easier to the eye, much less error prone, and it allows flexibility, since you don't need to change the props names or add props in the intermediate component when you change them.