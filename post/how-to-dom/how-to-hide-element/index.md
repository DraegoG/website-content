---
title: How to hide a DOM element using plain JavaScript
date: 2018-11-20T07:00:00+02:00
description: "Find out how to hide and then show again elements in vanilla JavaScript"
tags: js
---

How do you hide a DOM element using plain JavaScript?

Every element exposes a `style` property which you can use to alter the CSS styling properties.

You can set the `display` property to 'none' (like you would do in CSS, `display: none;`):

```js
element.style.display = 'none'
```

To display it again, set it back to `block` or `inline`:

```js
element.style.display = 'block'
```
