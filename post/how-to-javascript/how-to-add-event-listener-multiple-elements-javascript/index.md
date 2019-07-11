---
title: How to add an event listener to multiple elements in JavaScript
date: 2019-07-08T07:00:00+02:00
description: "Say you want to add an event listener to multiple elements in JavaScript. How can you do so?"
tags: js
---

In JavaScript you add an [event listener](/javascript-events/) to a single element using this syntax:

```js
document.querySelector('.my-element').addEventListener('click', event => {
  //handle click
})
```

But how can you attach the same event to multiple elements?

In other words, how to call `addEventListener()` on multiple elements at the same time?

You can do this in 2 ways. One is using a **loop**, the other is using **event bubbling**.

## Using a loop

The loop is the simplest one conceptually.

You can call `querySelectorAll()` on all elements with a specific class, then use `forEach()` to iterate on them:

```js
document.querySelectorAll('.some-class').forEach(item => {
  item.addEventListener('click', event => {
    //handle click
  }
})
```

If you don't have a common class for your elements you can build an array on the fly:

```js
[document.querySelector('.a-class'), document.querySelector('.another-class')].forEach(item => {
  item.addEventListener('click', event => {
    //handle click
  }
})
```

## Using event bubbling

Another option is to rely on [event bubbling](/javascript-events/#event-bubbling-and-event-capturing) and attach the event listener on the `body` element.

The event is always managed by the most specific element, so you can immediately check if that's one of the elements that should handle the event:

```js
const element1 = document.querySelector('.a-class')
const element2 = document.querySelector('.another-class')

body.addEventListener('click', event => {
  if (event.target !== element1 && event.target !== element2) {
    return
  }
  //handle click
}
```
