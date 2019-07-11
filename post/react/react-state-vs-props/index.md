---
title: "Props vs State in React"
date: 2018-11-08T07:00:00+02:00
description: "What's the difference between state and props in React?"
tags: react
---

In a React component, **props** are variables passed to it by its parent component.
**State** on the other hand is still variables, but directly initialized and managed by the component.

The state can be initialized by props.

For example, a parent component might include a child component by calling

```js
<ChildComponent />
```

The parent can pass a prop by using this syntax:

```js
<ChildComponent color=green />
```

Inside the ChildComponent constructor we could access the prop:

```js
class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
    console.log(props.color)
  }
}
```

and any other method in this class can reference the props using `this.props`.

Props can be used to set the internal state based on a prop value in the constructor, like this:

```js
class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state.colorName = props.color
  }
}
```

Of course a component can also initialize the state without looking at props.

In this case there's nothing useful going on, but imagine doing something different based on the prop value, probably setting a state value is best.

Props should never be changed in a child component, so if there's something going on that alters some variable, that variable should belong to the component state.

Props are also used to allow child components to access methods defined in the parent component. This is a good way to centralize managing the state in the parent component, and avoid children to have the need to have their own state.

Most of your components will just display some kind of information based on the props they received, and stay **stateless**.
