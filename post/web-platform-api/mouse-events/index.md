---
title: "Mouse events"
date: 2019-08-23T07:00:00+02:00
description: "Discover the basics of working with mouse events in JavaScript"
tags: browser
---

> See more on [JavaScript events](/javascript-events/)

When looking at mouse events we have the ability to interact with

- `mousedown` the mouse button was pressed
- `mouseup` the mouse button was released
- `click` a click event
- `dblclick` a double click event
- `mousemove` when the mouse is moved over the element
- `mouseover` when the mouse is moved over an element or one of its child elements
- `mouseenter` when the mouse is moved over an element. Similar to `mouseover` but does not bubble (more on this soon!)
- `mouseout` when the mouse is moved out of an element, and when the mouse enters a child elements
- `mouseleave` when the mouse is moved out of an element. Similar to `mouseout` but does not bubble (more on this soon!)
- `contextmenu` when the context menu is opened, e.g. on a right mouse button click

Events overlap. When you track a `click` event, it's like tracking a `mousedown` followed by a `mouseup` event. In the case of `dblclick`, `click` is also fired two times.

`mousedown`, `mousemove` and `mouseup` can be used in combination to track drag-and-drop events.

Be careful with `mousemove`, as it fires many times during the mouse movement. We need to apply **throttling**, which is something we'll talk more when we'll analyze scrolling.

When inside an eventh handler we have access to lots of properties.

For example on a mouse event we can check which mouse button was pressed by checking the `button` property of the event object:

```js
const link = document.getElementById('my-link')
link.addEventListener('mousedown', event => {
  // mouse button pressed
  console.log(event.button) //0=left, 2=right
})
```

Here are all the properties we can use:

- `altKey` true if alt key was pressed when the event was fired
- `button` if any, the number of the button that was pressed when the mouse event was fired (usually 0 = main button, 1 = middle button, 2 = right button). Works on events caused by clicking the button (e.g. clicks)
- `buttons` if any, a number indicating the button(s) pressed on any mouse event.
- `clientX` / `clientY` the x and y coordinates of the mouse pointer relative to the browser window, regardless of scrolling
- `ctrlKey` true if ctrl key was pressed when the event was fired
- `metaKey` true if meta key was pressed when the event was fired
- `movementX` / `movementY` the x and y coordinates of the mouse pointer relative to the position of the last mousemove event. Used to track the mouse velocity while moving it around
- `region` used in the Canvas API
- `relatedTarget` the secondary target for the event, for example when moving
- `screenX` / `screenY` the x and y coordinates of the mouse pointer in the screen coordinates
- `shiftKey` true if shift key was pressed when the event was fired
