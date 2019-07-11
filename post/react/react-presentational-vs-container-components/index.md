---
title: "React: Presentational vs Container Components"
date: 2018-12-21T07:00:00+02:00
description: "The difference between Presentational and Container Components in React"
tags: react
---

In React components are often divided into 2 big buckets: **presentational components** and **container components**.

Each of those have their unique characteristics.

Presentational components are mostly concerned with generating some markup to be outputted.

They don't manage any kind of state, except for state related the the presentation

Container components are mostly concerned with the "backend" operations.

They might handle the state of various sub-components.
They might wrap several presentational components.
They might interface with Redux.

As a way to simplify the distinction, we can say **presentational components are concerned with the look**, **container components are concerned with making things work**.

For example, this is a presentational component. It gets data from its props, and just focuses on showing an element:

```js
const Users = props => (
  <ul>
    {props.users.map(user => (
      <li>{user}</li>
    ))}
  </ul>
)
```

On the other hand this is a container component. It manages and stores its own data, and uses the presentational component to display it.

```js
class UsersContainer extends React.Component {
  constructor() {
    this.state = {
      users: []
    }
  }

  componentDidMount() {
    axios.get('/users').then(users =>
      this.setState({ users: users }))
    )
  }

  render() {
    return <Users users={this.state.users} />
  }
}
```
