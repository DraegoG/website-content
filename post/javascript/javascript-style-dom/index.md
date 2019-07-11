---
title: How to style DOM elements using JavaScript
date: 2019-01-21T07:00:00+02:00
description: "The ways you can apply styling to elements on the page, dynamically, using plain JavaScript"
tags: js
---

You might have the need to dynamically apply CSS properties to DOM elements.

What are the APIs browser expose to do that?

First, one of the cleanest ways is to add or remove classes from an element, and use classes styling in your CSS.

```js
const element = document.querySelector('#my-element')
```

You can use the `classList` property of an element and its `add()` and `remove()` methods:

```js
element.classList.add('myclass')
element.classList.remove('myclass')
```

You can also directly change each CSS property of an element by using the `style` property, which references the element **inline styles**.

For example you can change an element color using

```js
element.style.color = '#fff'
```

You can alter the border:

```js
element.style.border = '1px solid black'
```

You saw `color` and `border`. You can change all the CSS properties, by using camelCase instead of dashes when the CSS property name contains them.

A translation table is conveniently listed in [this MDN page](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference).