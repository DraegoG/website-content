---
title: "React Events"
date: 2018-10-28T07:00:00+02:00
description: "Learn how to interact with events in a React application"
tags: react
---

React provides an easy way to manage events. Prepare to say goodbye to `addEventListener`.

In the previous article about the State you saw this example:

```js
const CurrencySwitcher = props => {
  return (
    <button onClick={props.handleChangeCurrency}>
      Current currency is {props.currency}. Change it!
    </button>
  )
}
```

If you've been using JavaScript for a while, this is just like plain old [JavaScript event handlers](https://flaviocopes.com/javascript-events/), except that this time you're defining everything in JavaScript, not in your HTML, and you're passing a function, not a string.

The actual event names are a little bit different because in React you use camelCase for everything, so `onclick` becomes `onClick`, `onsubmit` becomes `onSubmit`.

For reference, this is old school HTML with JavaScript events mixed in:

```html
<button onclick="handleChangeCurrency()">...</button>
```

### Event handlers

It's a convention to have event handlers defined as methods on the Component class:

```js
class Converter extends React.Component {
  handleChangeCurrency = event => {
    this.setState({ currency: this.state.currency === '€' ? '$' : '€' })
  }
}
```

All handlers receive an event object that adheres, cross-browser, to the [W3C UI Events spec](https://www.w3.org/TR/DOM-Level-3-Events/).

### Bind `this` in methods

Don't forget to bind methods. The methods of ES6 classes by default are not bound. What this means is that `this` is not defined unless you define methods as arrow functions:

```js
class Converter extends React.Component {
  handleClick = e => {
    /* ... */
  }
  //...
}
```

when using the the property initializer syntax with Babel (enabled by default in `create-react-app`), otherwise you need to bind it manually in the constructor:

```js
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.handleClick = this.handleClick.bind(this)
  }
  handleClick(e) {}
}
```

### The events reference

There are lots of events supported, here's a summary list.

#### Clipboard

- onCopy
- onCut
- onPaste

#### Composition

- onCompositionEnd
- onCompositionStart
- onCompositionUpdate

#### Keyboard

- onKeyDown
- onKeyPress
- onKeyUp

#### Focus

- onFocus
- onBlur

#### Form

- onChange
- onInput
- onSubmit

#### Mouse

- onClick
- onContextMenu
- onDoubleClick
- onDrag
- onDragEnd
- onDragEnter
- onDragExit
- onDragLeave
- onDragOver
- onDragStart
- onDrop
- onMouseDown
- onMouseEnter
- onMouseLeave
- onMouseMove
- onMouseOut
- onMouseOver
- onMouseUp

#### Selection

- onSelect

#### Touch

- onTouchCancel
- onTouchEnd
- onTouchMove
- onTouchStart

#### UI

- onScroll

#### Mouse Wheel

- onWheel

#### Media

- onAbort
- onCanPlay
- onCanPlayThrough
- onDurationChange
- onEmptied
- onEncrypted
- onEnded
- onError
- onLoadedData
- onLoadedMetadata
- onLoadStart
- onPause
- onPlay
- onPlaying
- onProgress
- onRateChange
- onSeeked
- onSeeking
- onStalled
- onSuspend
- onTimeUpdate
- onVolumeChange
- onWaiting

#### Image

- onLoad
- onError

#### Animation

- onAnimationStart
- onAnimationEnd
- onAnimationIteration

#### Transition

- onTransitionEnd
