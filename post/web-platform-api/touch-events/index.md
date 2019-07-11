---
title: "Touch events"
date: 2019-08-27T07:00:00+02:00
description: "Discover the basics of working with touch events in JavaScript"
tags: browser
---

> See more on [JavaScript events](/javascript-events/)

Touch events are those events that are triggered when viewing the page on a mobile device, like a smartphone or a tablet.

They allow you to track multitouch events.

We have 4 touch events:

- `touchstart` a touch event has started (the surface is touched)
- `touchend` a touch event has ended (the surface is no longer touched)
- `touchmove` the finger (or whatever is touching the device) moves over the surface
- `touchcancel` the touch event has been cancelled

Every time a touch event occurs we are passed a [touch event](https://developer.mozilla.org/en-US/docs/Web/API/Touch):

```js
const link = document.getElementById('my-link')
link.addEventListener('touchstart', event => {
  // touch event started
})
```

Here are all the properties we can access on that event

- `identifier` an unique identifier for this specific event. Used to track multi-touch events. Same finger = same identifier.
- `clientX` / `clientY` the x and y coordinates of the mouse pointer relative to the browser window, regardless of scrolling
- `screenX` / `screenY` the x and y coordinates of the mouse pointer in the screen coordinates
- `pageX` / `pageY` the x and y coordinates of the mouse pointer in the page coordinates (including scrolling)
- `target` the element touched
