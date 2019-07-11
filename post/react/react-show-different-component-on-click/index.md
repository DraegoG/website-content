---
title: "React: How to show a different component on click"
date: 2018-11-05T07:00:00+02:00
description: "Toggle the visibility of components by telling React to display another component when you click something"
tags: react
---

In many scenarios you want to display a completely different component inside a screen, when a button or link is clicked.

Think about a navigation structure, for example.

How can you do so?

> In this example I'm managing the state centralized in the App component.

First, attach a click event to a component:

```js
import React from 'react'

const AddTripButton = props => {
  return <button onClick={props.addTrip}>Add a trip</button>
}

export default AddTripButton
```

Then in the App component, handle the addTrip event by assigning it the `triggerAddTripState` method:

```js
<AddTripButton addTrip={this.triggerAddTripState} />
```

In `triggerAddTripState` you edit the state of the component:

```js

class App extends Component {
  constructor(props) {
    super(props)
    this.state = { isEmptyState: true }
  }

  triggerAddTripState = () => {
    this.setState({
      ...this.state,
      isEmptyState: false,
      isAddTripState: true
    })
  }
}
```

See, here I create a default state, which contains `isEmptyState: true`. When the `triggerAddTripState` method is run, the state is edited so that property is set to false, and a new `isAddTripState` property is set to true.

Now in the JSX we can use those 2 state properties to show and hide parts of the component by using this syntax:

```js
render() {
  return (
    <div>
      {this.state.isEmptyState && <AddTripButton addTrip={this.triggerAddTripState} />}

      {this.state.isAddTripState && <AnotherComponent />}
    </div>
  )
}
```