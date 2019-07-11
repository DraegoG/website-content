---
title: CSS Box Sizing
date: 2019-06-16T07:00:00+02:00
description: "How to work with box sizing in CSS"
tags: css
---

The default behavior of browsers when calculating the width of an element is to apply the calculated width and height to the **content area**, without taking any of the padding, border and margin in consideration.

This approach has proven to be quite complicated to work with.

You can change this behavior by setting the `box-sizing` property.

The `box-sizing` property is a great help. It has 2 values:

- `border-box`
- `content-box`

`content-box` is the default, the one we had for ages before `box-sizing` became a thing.

`border-box` is the new and great thing we are looking for. If you set that on an element:

```css
.my-div {
  box-sizing: border-box;
}
```

width and height calculation include the padding and the border. Only the margin is left out, which is reasonable since in our mind we also typically see that as a separate thing: margin is outside of the box.

This property is a small change but has a big impact. CSS Tricks even declared an [international box-sizing awareness day](https://css-tricks.com/international-box-sizing-awareness-day/), just saying, and it's recommended to apply it to every element on the page, out of the box, with this:

```css
*, *:before, *:after {
  box-sizing: border-box;
}
```