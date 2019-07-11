---
title: "React Concept: Composition"
date: 2018-12-20T07:00:00+02:00
description: "What is composition and why is it a key concept in your React apps"
tags: react
---

In programming, composition allows you to build more complex functionality by combining small and focused functions.

For example, think about using `map()` to create a new array from an initial set, and then filtering the result using `filter()`:

```js
const list = ['Apple', 'Orange', 'Egg']
list.map(item => item[0]).filter(item => item === 'A') //'A'
```

In React, composition allows you to have some pretty cool advantages.

You create small and lean components and use them to _compose_ more functionality on top of them. How?

## Create specialized version of a component

Use an outer component to expand and specialize a more generic component:

```js
const Button = props => {
  return <button>{props.text}</button>
}

const SubmitButton = () => {
  return <Button text="Submit" />
}

const LoginButton = () => {
  return <Button text="Login" />
}
```

## Pass methods as props

A component can focus on tracking a click event, for example, and what actually happens when the click event happens is up to the container component:

```js
const Button = props => {
  return <button onClick={props.onClickHandler}>{props.text}</button>
}

const LoginButton = props => {
  return <Button text="Login" onClickHandler={props.onClickHandler} />
}

const Container = () => {
  const onClickHandler = () => {
    alert('clicked')
  }

  return <LoginButton onClickHandler={onClickHandler} />
}
```

## Using children

The `props.children` property allows you to inject components inside other components.

The component needs to output `props.children` in its JSX:

```js
const Sidebar = props => {
  return <aside>{props.children}</aside>
}
```

and you embed more components into it in a transparent way:

```js
<Sidebar>
  <Link title="First link" />
  <Link title="Second link" />
</Sidebar>
```

## Higher order components

When a component receives a component as a prop and returns a component, it's called higher order component.

We'll see them in a little while.
