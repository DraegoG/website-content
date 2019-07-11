---
title: CSS Backgrounds
seotitle: The CSS Backgrounds Tutorial
date: 2019-06-19T07:00:00+02:00
description: "Learn how to change the background of an element using CSS"
tags: css
---

The background of an element can be changed  using several CSS properties:

- `background-color`
- `background-image`
- `background-clip`
- `background-position`
- `background-origin`
- `background-repeat`
- `background-attachment`
- `background-size`

and the shorthand property `background`, which allows to shorten definitions and group them on a single line.

`background-color` accepts a color value, which can be one of the color keywords, or an `rgb` or `hsl` value:

```css
p {
  background-color: yellow;
}

div {
  background-color: #333;
}
```

Instead of using a color, you can use an image as background to an element, by specifying the image location URL:

```css
div {
  background-image: url(image.png);
}
```

`background-clip` lets you determine the area used by the background image, or color. The default value is `border-box`, which extends up to the border outer edge.

Other values are

- `padding-box` to extend the background up to the padding edge, without the border
- `content-box` to extend the background up to the content edge, without the padding
- `inherit` to apply the value of the parent

When using an image as background you will want to set the position of the image placement using the `background-position` property: `left`, `right`, `center` are all valid values for the X axis, and `top`, `bottom` for the Y axis:

```css
div {
  background-position: top right;
}
```

If the image is smaller than the background, you need to set the behavior using `background-repeat`. Should it `repeat-x`, `repeat-y` or `repeat` on all the axis? This last one is the default value. Another value is `no-repeat`.

`background-origin` lets you choose where the background should be applied: to the entire element including padding (default) using `padding-box`, to the entire element including the border using `border-box`, to the element without the padding using `content-box`.

With `background-attachment` we can attach the background to the viewport, so that scrolling will not affect the background:

```css
div {
  background-attachment: fixed;
}
```

By default the value is `scroll`. There is another value, `local`. The best way to visualize their behavior is [this Codepen](https://codepen.io/BernLeech/pen/mMNKJV).

The last background property is `background-size`. We can use 3 keywords: `auto`, `cover` and `contain`. `auto` is the default.

`cover` expands the image until the entire element is covered by the background.

`contain` stops expanding the background image when one dimension (x or y) covers the whole smallest edge of the image, so it's fully contained into the element.

You can also specify a length value, and if so it sets the width of the background image (and the height is automatically defined):

```css
div {
  background-size: 100%;
}
```

If you specify 2 values, one is the width and the second is the height:

```css
div {
  background-size: 800px 600px;
}
```

The shorthand property `background`  allows to shorten definitions and group them on a single line.

This is an example:

```css
div {
  background: url(bg.png) top left no-repeat;
}
```

If you use an image, and the image could not be loaded, you can set a fallback color:

```css
div {
  background: url(image.png) yellow;
}
```

You can also set a gradient as background:

```css
div {
  background: linear-gradient(#fff, #333);
}
```

