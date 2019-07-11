---
title: How to wait for the DOM ready event in plain JavaScript
description: "How to run JavaScript as soon as we can, but not sooner"
date: 2018-10-17T07:00:00+02:00
tags: browser
---

You can do so by adding an event listener to the `document` object for the `DOMContentLoaded` event:

```js
document.addEventListener('DOMContentLoaded', (event) => {
  //the event occurred
})
```

I usually don't use arrow functions inside for the event callback, because we cannot access `this`.

In this case we don't need so, because `this` is always `document`. In any other event listener I would just use a regular function:

```js
document.addEventListener('DOMContentLoaded', function(event) {
  //the event occurred
})
```

for example if I'm adding the event listener inside a loop and I don't really know what `this` will be when the event is triggered.