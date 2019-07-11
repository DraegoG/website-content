---
title: How to add a click event to a list of DOM elements returned from querySelectorAll
description: "How to iterate a NodeList and attach an event listener to each element"
date: 2018-10-24T07:00:00+02:00
tags: browser
---

You can add an event listener to all the elements returned by a `document.querySelectorAll()` call by iterating over those results using the `for..of` loop:

```js
const buttons = document.querySelectorAll("#select .button")
for (const button of buttons) {
  button.addEventListener('click', function(event) {
    //...
  })
}
```

It's important to note that `document.querySelectorAll()` does not return an array, but a NodeList object.

You can iterate it with `forEach` or `for..of`, or you can transform it to an array with `Array.from()` if you want.