---
title: "The React State"
date: 2018-10-29T07:00:00+02:00
description: "How to interact with the state of your components"
tags: react
---

### Setting the default state

In the Component constructor, initialize `this.state`. For example the BlogPostExcerpt component might have a `clicked` state:

```js
class BlogPostExcerpt extends Component {
  constructor(props) {
    super(props)
    this.state = { clicked: false }
  }

  render() {
    return (
      <div>
        <h1>Title</h1>
        <p>Description</p>
      </div>
    )
  }
}
```

### Accessing the state

The _clicked_ state can be accessed by referencing `this.state.clicked`:

```js
class BlogPostExcerpt extends Component {
  constructor(props) {
    super(props)
    this.state = { clicked: false }
  }

  render() {
    return (
      <div>
        <h1>Title</h1>
        <p>Description</p>
        <p>Clicked: {this.state.clicked}</p>
      </div>
    )
  }
}
```

### Mutating the state

A state should never be mutated by using

```js
this.state.clicked = true
```

Instead, you should always use `setState()` instead, passing it an object:

```js
this.setState({ clicked: true })
```

The object can contain a subset, or a superset, of the state. Only the properties you pass will be mutated, the ones omitted will be left in their current state.

#### Why you should always use `setState()`

The reason is that using this method, React knows that the state has changed. It will then start the series of events that will lead to the Component being re-rendered, along with any [DOM](https://flaviocopes.com/dom/) update.

### Unidirectional Data Flow

A state is always owned by one Component. Any data that's affected by this state can only affect Components below it: its children.

Changing the state on a Component will never affect its parent, or its siblings, or any other Component in the application: just its children.

This is the reason the state is often moved up in the Component tree.

### Moving the State Up in the Tree

Because of the Unidirectional Data Flow rule, if two components need to share state, the state needs to be moved up to a common ancestor.

Many times the closest ancestor is the best place to manage the state, but it's not a mandatory rule.

The state is passed down to the components that need that value via props:

```js
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.state = { currency: '€' }
  }

  render() {
    return (
      <div>
        <Display currency={this.state.currency} />
        <CurrencySwitcher currency={this.state.currency} />
      </div>
    )
  }
}
```

The state can be mutated by a child component by passing a mutating function down as a prop:

```js
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.state = { currency: '€' }
  }

  handleChangeCurrency = event => {
    this.setState({ currency: this.state.currency === '€' ? '$' : '€' })
  }

  render() {
    return (
      <div>
        <Display currency={this.state.currency} />
        <CurrencySwitcher
          currency={this.state.currency}
          handleChangeCurrency={this.handleChangeCurrency}
        />
      </div>
    )
  }
}

const CurrencySwitcher = props => {
  return (
    <button onClick={props.handleChangeCurrency}>
      Current currency is {props.currency}. Change it!
    </button>
  )
}

const Display = props => {
  return <p>Current currency is {props.currency}.</p>
}
```
