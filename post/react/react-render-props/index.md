---
title: "React Render Props"
date: 2019-01-01T07:00:00+02:00
description: "Learn how Render Props can help you build a React application"
tags: react
---

A common pattern used to share state between components is to use the `children` prop.

Inside a component JSX you can render `{this.props.children}` which automatically injects any JSX passed in the parent component as a children:

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      /*...*/
    }
  }

  render() {
    return <div>{this.props.children}</div>
  }
}

const Children1 = () => {}

const Children2 = () => {}

const App = () => (
  <Parent>
    <Children1 />
    <Children2 />
  </Parent>
)
```

However, there is a problem here: the state of the parent component cannot be accessed from the children.

To be able to share the state, you need to use a render prop component, and instead of passing components as children of the parent component, you pass a function which you then execute in `{this.props.children()}`. The function can accept arguments, :

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: 'Flavio' }
  }

  render() {
    return <div>{this.props.children(this.state.name)}</div>
  }
}

const Children1 = props => {
  return <p>{props.name}</p>
}

const App = () => <Parent>{name => <Children1 name={name} />}</Parent>
```

Instead of using the `children` prop, which has a very specific meaning, you can use any prop, and so you can use this pattern multiple times on the same component:

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
    this.state = { name: 'Flavio', age: 35 }
  }

  render() {
    return (
      <div>
        <p>Test</p>
        {this.props.someprop1(this.state.name)}
        {this.props.someprop2(this.state.age)}
      </div>
    )
  }
}

const Children1 = props => {
  return <p>{props.name}</p>
}

const Children2 = props => {
  return <p>{props.age}</p>
}

const App = () => (
  <Parent
    someprop1={name => <Children1 name={name} />}
    someprop2={age => <Children2 age={age} />}
  />
)

ReactDOM.render(<App />, document.getElementById('app'))
```
