---
title: "The Virtual DOM"
date: 2018-10-27T07:00:00+02:00
description: "The Virtual DOM is a technique that React uses to optimize interacting with the browser"
tags: react
---

Many existing frameworks, before React came on the scene, were directly manipulating the DOM on every change.

First, what is the DOM?

The DOM (_Document Object Model_) is a Tree representation of the page, starting from the `<html>` tag, going down into every child, which are called nodes.

It's kept in the browser memory, and directly linked to what you see in a page.
The DOM has an API that you can use to traverse it, access every single node, filter them, modify them.

The API is the familiar syntax you have likely seen many times, if you were not using the abstract API provided by jQuery and friends:

```js
document.getElementById(id)
document.getElementsByTagName(name)
document.createElement(name)
parentNode.appendChild(node)
element.innerHTML
element.style.left
element.setAttribute()
element.getAttribute()
element.addEventListener()
window.content
window.onload
window.dump()
window.scrollTo()
```

React keeps a copy of the DOM representation, for what concerns the React rendering: the Virtual DOM

### The Virtual DOM Explained

Every time the DOM changes, the browser has to do two intensive operations: repaint (visual or content changes to an element that do not affect the layout and positioning relative to other elements) and reflow (recalculate the layout of a portion of the page - or the whole page layout).

React uses a Virtual DOM to help the browser use less resources when changes need to be done on a page.

When you call `setState()` on a Component, specifying a state different than the previous one, React marks that Component as **dirty**. This is key: React only updates when a Component changes the state explicitly.

What happens next is:

- React updates the Virtual DOM relative to the components marked as dirty (with some additional checks, like triggering `shouldComponentUpdate()`)
- Runs the diffing algorithm to reconcile the changes
- Updates the real DOM

### Why is the Virtual DOM helpful: batching

The key thing is that React batches much of the changes and performs a unique update to the real DOM, by changing all the elements that need to be changed at the same time, so the repaint and reflow the browser must perform to render the changes are executed just once.
