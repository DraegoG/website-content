---
title: "Learn how to use Redux"
seotitle: "Redux Tutorial: a guide for beginners"
date: 2018-01-28T09:06:15+02:00
updated: 2018-05-13T09:06:15+02:00
description: "Redux is a state manager that's usually used along with React, but it's not tied to that library. Learn Redux by reading this simple and easy to follow guide"
booktitle: "Redux"
bookdescription: " "
medium: true
tags: react

---

<!-- TOC -->

- [Why you need Redux](#Why-you-need-Redux)
- [When should you use Redux?](#When-should-you-use-Redux)
- [Immutable State Tree](#Immutable-State-Tree)
- [Actions](#Actions)
  - [Actions types should be constants](#Actions-types-should-be-constants)
  - [Action creators](#Action-creators)
- [Reducers](#Reducers)
  - [What is a reducer](#What-is-a-reducer)
  - [What a reducer should not do](#What-a-reducer-should-not-do)
  - [Multiple reducers](#Multiple-reducers)
  - [A simulation of a reducer](#A-simulation-of-a-reducer)
    - [The state](#The-state)
    - [A list of actions](#A-list-of-actions)
    - [A reducer for every part of the state](#A-reducer-for-every-part-of-the-state)
    - [A reducer for the whole state](#A-reducer-for-the-whole-state)
- [The Store](#The-Store)
  - [Can I initialize the store with server-side data?](#Can-I-initialize-the-store-with-server-side-data)
  - [Getting the state](#Getting-the-state)
  - [Update the state](#Update-the-state)
  - [Listen to state changes](#Listen-to-state-changes)
- [Data Flow](#Data-Flow)

<!-- /TOC -->

## Why you need Redux

Redux is a state manager that's usually used along with React, but it's not tied to that library - it can be used with other technologies as well, but we'll stick to React for the sake of the explanation.

React has its own way to manage state, as you can read on the [React Beginner's Guide](https://flaviocopes.com/react/), where I introduce how you can manage State in React.

Moving the state up in the tree works in simple cases, but in a complex app you might find you are moving almost all the state up, and then down using props.

React in version 16.3.0 introduced the [**Context API**](https://flaviocopes.com/react/#the-context-api), which makes Redux redundant for the use case of accessing the state from different parts of your app, so consider using the Context API instead of Redux, unless you need a specific feature that Redux provides.

Redux is a way to manage an application state, and move it to an **external global store**.

There are a few concepts to grasp, but once you do, Redux is a very simple approach to the problem.

Redux is very popular with React applications, but it's in no way unique to React: there are bindings for nearly any popular framework. That said, I'll make some examples using React as it is its primary use case.

## When should you use Redux?

Redux is ideal for medium to big apps, and you should only use it when you have trouble managing the state with the default state management of React, or the other library you use.

Simple apps should not need it at all (and there's nothing wrong with simple apps).

## Immutable State Tree

In Redux, the whole state of the application is represented by **one** [JavaScript](https://flaviocopes.com/javascript/) object, called **State** or **State Tree**.

We call it **Immutable State Tree** because it is read only: it can't be changed directly.

It can only be changed by dispatching an **Action**.

## Actions

An **Action** is **a JavaScript object that describes a change in a minimal way** (with just the information needed):

```js
{
  type: 'CLICKED_SIDEBAR'
}

// e.g. with more data
{
  type: 'SELECTED_USER',
  userId: 232
}
```

The only requirement of an action object is having a `type` property, whose value is usually a string.

### Actions types should be constants

In a simple app an action type can be defined as a string.

When the app grows is best to use constants:

```js
const ADD_ITEM = 'ADD_ITEM'
const action = { type: ADD_ITEM, title: 'Third item' }
```

and to separate actions in their own files, and import them

```js
import { ADD_ITEM, REMOVE_ITEM } from './actions'
```

### Action creators

**Actions Creators** are functions that create actions.

```js
function addItem(t) {
  return {
    type: ADD_ITEM,
    title: t
  }
}
```

You usually run action creators in combination with triggering the dispatcher:

```js
dispatch(addItem('Milk'))
```

or by defining an action dispatcher function:

```js
const dispatchAddItem = i => dispatch(addItem(i))
dispatchAddItem('Milk')
```

## Reducers

When an action is fired, something must happen, the state of the application must change.

This is the job of **reducers**.

### What is a reducer

A **reducer** is a **pure function** that calculates the next State Tree based on the previous State Tree, and the action dispatched.

```js
;(currentState, action) => newState
```

A pure function takes an input and returns an output without changing the input or anything else. Thus, a reducer returns a completely new state that substitutes the previous one.

### What a reducer should not do

A reducer should be a pure function, so it should:

- never mutate its arguments
- never mutate the state, but instead create a new one with `Object.assign({}, ...)`
- never generate side-effects (no API calls changing anything)
- never call non-pure functions, functions that change their output based on factors other than their input (e.g. `Date.now()` or `Math.random()`)

There is no reinforcement, but you should stick to the rules.

### Multiple reducers

Since the state of a complex app could be really wide, there is not a single reducer, but many reducers for any kind of action.

### A simulation of a reducer

At its core, Redux can be simplified with this simple model:

#### The state

```js
{
  list: [
    { title: "First item" },
    { title: "Second item" },
  ],
  title: 'Groceries list'
}
```

#### A list of actions

```js
{ type: 'ADD_ITEM', title: 'Third item' }
{ type: 'REMOVE_ITEM', index: 1 }
{ type: 'CHANGE_LIST_TITLE', title: 'Road trip list' }
```

#### A reducer for every part of the state

```js
const title = (state = '', action) => {
    if (action.type === 'CHANGE_LIST_TITLE') {
      return action.title
    } else {
      return state
    }
}

const list = (state = [], action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      return state.concat([{ title: action.title }])
    case 'REMOVE_ITEM':
      return state.filter(item =>
        action.index !== item.index)
    default:
      return state
  }
}
```

#### A reducer for the whole state

```js
const listManager = (state = {}, action) => {
  return {
    title: title(state.title, action),
    list: list(state.list, action)
  }
}
```

## The Store

The **Store** is an object that:

- **holds the state** of the app
- **exposes the state** via `getState()`
- allows us to **update the state** via `dispatch()`
- allows us to (un)register a **state change listener** using `subscribe()`

A store is **unique** in the app.

Here is how a store for the listManager app is created:

```js
import { createStore } from 'redux'
import listManager from './reducers'
let store = createStore(listManager)
```

### Can I initialize the store with server-side data?

Sure, **just pass a starting state**:

```js
let store = createStore(listManager, preexistingState)
```

### Getting the state

```js
store.getState()
```

### Update the state

```js
store.dispatch(addItem('Something'))
```

### Listen to state changes

```js
const unsubscribe = store.subscribe(() =>
  const newState = store.getState()
)

unsubscribe()
```

## Data Flow

Data flow in Redux is always **unidirectional**.

You call `dispatch()` on the Store, passing an Action.

The Store takes care of passing the Action to the Reducer, generating the next State.

The Store updates the State and alerts all the Listeners.
