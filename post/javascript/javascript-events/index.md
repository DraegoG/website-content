---
title: "JavaScript Events Explained"
description: "JavaScript in the browser uses an event-driven programming model. Everything starts by following an event. This is an introduction to JavaScript events and how event handling works"
date: 2018-04-10T07:06:29+02:00
updated: 2018-05-29T07:06:29+02:00
booktitle: "Events"
tags: js
tags_weight: 17
---

<!-- TOC -->

- [Introduction](#introduction)
- [Event handlers](#event-handlers)
  - [Inline event handlers](#inline-event-handlers)
  - [DOM on-event handlers](#dom-on-event-handlers)
  - [Using `addEventListener()`](#using-addeventlistener)
- [Listening on different elements](#listening-on-different-elements)
- [The Event object](#the-event-object)
- [Event bubbling and event capturing](#event-bubbling-and-event-capturing)
- [Stopping the propagation](#stopping-the-propagation)
- [Popular events](#popular-events)
  - [Load](#load)
  - [Mouse events](#mouse-events)
  - [Keyboard events](#keyboard-events)
  - [Scroll](#scroll)
- [Throttling](#throttling)

<!-- /TOC -->

## Introduction

JavaScript in the browser uses an event-driven programming model.

Everything starts by following an event.

The event could be the DOM is loaded, or an asynchronous request that finishes fetching, or a user clicking an element or scrolling the page, or the user types on the keyboard.

There are a lot of different kind of events.

## Event handlers

You can respond to any event using an **Event Handler**, which is a function that's called when an event occurs.

You can register multiple handlers for the same event, and they will all be called when that event happens.

JavaScript offer three ways to register an event handler:

### Inline event handlers

This style of event handlers is very rarely used today, due to its constraints, but it was the only way in the JavaScript early days:

```html
<a href="site.com" onclick="dosomething();">A link</a>
```

### DOM on-event handlers

This is common when an object has at most one event handler, as there is no way to add multiple handlers in this case:

```js
window.onload = () => {
  //window loaded
}
```

It's most commonly used when handling [XHR](/xhr/) requests:

```js
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  //.. do something
}
```

You can check if an handler is already assigned to a property using `if ('onsomething' in window) {}`.

### Using `addEventListener()`

This is the _modern way_. This method allows to register as many handlers as we need, and it's the most popular you will find:

```js
window.addEventListener('load', () => {
  //window loaded
})
```

This method allows to register as many handlers as we need, and it's the most popular you will find.

> Note that IE8 and below did not support this, and instead used its own `attachEvent()` API. Keep it in mind if you need to support older browsers.

## Listening on different elements

You can listen on `window` to intercept "global" events, like the usage of the keyboard, and you can listen on specific elements to check events happening on them, like a mouse click on a button.

This is why `addEventListener` is sometimes called on `window`, sometimes on a DOM element.

## The Event object

An event handler gets an `Event` object as the first parameter:

```js
const link = document.getElementById('my-link')
link.addEventListener('click', event => {
  // link clicked
})
```

This object contains a lot of useful properties and methods, like:

- `target`, the DOM element that originated the event
- `type`, the type of event
- `stopPropagation()`, called to stop propagating the event in the DOM

([see the full list](https://developer.mozilla.org/en-US/docs/Web/API/Event)).

Other properties are provided by specific kind of events, as `Event` is an interface for different specific events:

- [MouseEvent](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)
- [KeyboardEvent](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent)
- [DragEvent](https://developer.mozilla.org/en-US/docs/Web/API/DragEvent)
- [FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)
- ... and others

Each of those has a MDN page linked, so you can inspect all their properties.

For example when a KeyboardEvent happens, you can check which key was pressed, in ar readable format (`Escape`, `Enter` and so on) by checking the `key` property:

```js
window.addEventListener('keydown', event => {
  // key pressed
  console.log(event.key)
})
```

On a mouse event we can check which mouse button was pressed:

```js
const link = document.getElementById('my-link')
link.addEventListener('mousedown', event => {
  // mouse button pressed
  console.log(event.button) //0=left, 2=right
})
```

## Event bubbling and event capturing

Bubbling and capturing are the 2 models that events use to propagate.

Suppose you DOM structure is

```html
<div id="container">
  <button>Click me</button>
</div>
```

You want to track when users click on the button, and you have 2 event listeners, one on `button`, and one on `#container`. Remember, a click on a child element will always propagate to its parents, unless you stop the propagation (see later).

Those event listeners will be called in order, and this order is determined by the event bubbling/capturing model used.

**Bubbling** means that the event propagates from the item that was clicked (the child) up to all its parent tree, starting from the nearest one.

In our example, the handler on `button` will fire before the `#container` handler.

**Capturing** is the opposite: the outer event handlers are fired before the more specific handler, the one on `button`.

**By default all events bubble**.

You can choose to adopt event capturing by applying a third argument to addEventListener, setting it to `true`:

```js
document.getElementById('container').addEventListener(
  'click',
  () => {
    //window loaded
  },
  true
)
```

Note that **first all capturing event handlers are run**.

Then all the bubbling event handlers.

The order follows this principle: the DOM goes through all elements starting from the Window object, and goes to find the item that was clicked. While doing so, it calls any event handler associated to the event (capturing phase).

Once it reaches the target, it then repeats the journey up to the parents tree until the Window object, calling again the event handlers (bubbling phase).

## Stopping the propagation

An event on a DOM element will be propagated to all its parent elements tree, unless it's stopped.

```html
<html>
  <body>
    <section>
      <a id="my-link" ...>
```

A click event on `a` will propagate to `section` and then `body`.

You can stop the propagation by calling the `stopPropagation()` method of an Event, usually at the end of the event handler:

```js
const link = document.getElementById('my-link')
link.addEventListener('mousedown', event => {
  // process the event
  // ...

  event.stopPropagation()
})
```

## Popular events

Here's a list of the most common events you will likely handle.

### Load

`load` is fired on `window` and the `body` element when the page has finished loading.

### Mouse events

`click` fires when a mouse button is clicked. `dblclick` when the mouse is clicked two times. Of course in this case `click` is fired just before this event.
`mousedown`, `mousemove` and `mouseup` can be used in combination to track drag-and-drop events. Be careful with `mousemove`, as it fires many times during the mouse movement (see _throttling_ later)

### Keyboard events

`keydown` fires when a keyboard button is pressed (and any time the key repeats while the button _stays_ pressed). `keyup` is fired when the key is released.

### Scroll

The `scroll` event is fired on `window` every time you scroll the page. Inside the event handler you can check the current scrolling position by checking `window.scrollY`.

Keep in mind that this event is not a one-time thing. It fires a lot of times during scrolling, not just at the end or beginning of the scrolling, so don't do any heavy computation or manipulation in the handler - use _throttling_ instead.

## Throttling

As we mentioned above, `mousemove` and `scroll` are two events that are not fired one-time per event, but rather they continuously call their event handler function during all the duration of the action.

This is because they provide coordinates so you can track what's happening.

If you perform a complex operation in the event handler, you will affect the performance and cause a sluggish experience to your site users.

Libraries that provide throttling like [Lodash](https://lodash.com/docs/4.17.10#throttle) implement it in 100+ lines of code, to handle every possible use case. A simple and easy to understand implementation is this, which uses [setTimeout](/javascript-timers/) to cache the scroll event every 100ms:

```js
let cached = null
window.addEventListener('scroll', event => {
  if (!cached) {
    setTimeout(() => {
      //you can access the original event at `cached`
      cached = null
    }, 100)
  }
  cached = event
})
```
