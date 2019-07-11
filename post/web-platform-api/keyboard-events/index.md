---
title: "Keyboard events"
date: 2019-08-19T07:00:00+02:00
description: "Discover the basics of working with keyboard events in JavaScript"
tags: browser
---

There are 3 types of events when interacting with keyboard events:

- `keydown` the keyboard key has been pressed
- `keyup` the keyboard key has been released

`keydown` is also fired when the key repeats while the button _stays_ pressed.

While mouse and touch events are typically listened on a specific element, it's common to listen for keyboard events on the **document**:

```js
document.addEventListener('keydown', event => {
  // key pressed
})
```

The parameter passed to the event listener is a [KeyboardEvent](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent).

This event object, in addition to the [Event object properties](https://developer.mozilla.org/en-US/docs/Web/API/Event) offers us (among others) these unique properties:

- `altKey` true if alt key was pressed when the event was fired
- `code` the code of the key pressed, returned as a string
- `ctrlKey` true if ctrl key was pressed when the event was fired
- `key` the value of the key pressed, returned as a string
- `locale` the keyboard locale value
- `location` the [location of the key](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/location) on the keyboard
- `metaKey` true if meta key was pressed when the event was fired
- `repeat` true if the key has been repeated (e.g. the key has not been released)
- `shiftKey` true if shift key was pressed when the event was fired

This demo is a keylogger which will show you the values of some of the properties I listed above:

<p class="codepen" data-height="725" data-theme-id="0" data-default-tab="result" data-user="flaviocopes" data-slug-hash="LopWmq" style="height: 725px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Key logger demo">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/LopWmq/">
  Key logger demo</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

