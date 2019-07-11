---
title: "React Portals"
date: 2018-12-31T07:00:00+02:00
description: "Find out how to use React Portals"
tags: react
---

React 16, released in September 2017, introduced Portals.

A portal is a way to render an element outside of its component hierarchy, in a separate component.

When that event is rendered, events happening on it are managed by the React components hierarchy rather than by the hierarchy set by the DOM position of the element.

Hence the name "portal": an element sits somewhere in the DOM tree that's outside of the normal React components tree, but the React component tree that includes it is still in charge.

React offers an easy API to do this, `ReactDOM.createPortal()`, which accepts 2 arguments. The first is the element to render, the second is the DOM element where to render it.

A classic use case for this is modal windows.

A modal to render at full screen must live outside of the element, so it can be properly styled using CSS.

So if a modal is defined as a component:

```js
class Modal extends React.Component {
  constructor(props) {
    super(props)
    this.el = document.createElement('div')
  }

  componentDidMount() {
    document.getElementById('modal').appendChild(this.el)
  }

  componentWillUnmount() {
    document.getElementById('modal').removeChild(this.el)
  }

  render() {
    return ReactDOM.createPortal(
      this.props.children,
      this.el
    )
  }
}
```

We can have an App component render it, and all the events happening in the Modal component will be handled by App even though technically the modal is rendered in a different DOM tree:

```js
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {showModal: false}

    this.handleShow = this.handleShow.bind(this)
    this.handleHide = this.handleHide.bind(this)
  }

  handleShow() {
    this.setState({showModal: true})
  }

  handleHide() {
    this.setState({showModal: false})
  }

  render() {
    const modal = this.state.showModal ? (
      <Modal>
        <div>
          The modal <button onClick={this.handleHide}>Hide</button>
        </div>
      </Modal>
    ) : ''

    return (
      <div>
        The app <button onClick={this.handleShow}>Show modal</button>
        {modal}
      </div>
    )
  }
}

ReactDOM.render(<App />, document.getElementById('app'))
```

See the full example on <https://codepen.io/flaviocopes/pen/KbdagX>