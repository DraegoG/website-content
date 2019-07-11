---
title: CSS Filters
seotitle: The CSS Filters Tutorial
date: 2019-06-14T07:00:00+02:00
description: "How to work with the CSS `filter` property"
tags: css
---

Filters allow us to perform operations on elements.

Things you normally do with Photoshop or other photo editing software, like changing the opacity or the brightness, and more.

You use the `filter` property. Here's an example of it applied on an image, but this property can be used on _any_ element:

```css
img {
  filter: <something>;
}
```

You can use various values here:

- `blur()`
- `brightness()`
- `contrast()`
- `drop-shadow()`
- `grayscale()`
- `hue-rotate()`
- `invert()`
- `opacity()`
- `sepia()`
- `saturate()`
- `url()`

Notice the parentheses after each option, because they all require a parameter.

For example:

```css
img {
  filter: opacity(0.5);
}
```

means the image will be 50% transparent, because `opacity()` takes one value from 0 to 1, or a percentage.

You can also apply multiple filters at once:

```css
img {
  filter: opacity(0.5) blur(2px);
}
```

Let's now talk about each filter in details.

### `blur()`

Blurs an element content. You pass it a value, expressed in `px` or `em` or `rem` that will be used to determine the blur radius.

Example:

```css
img {
  filter: blur(4px);
}
```

### `opacity()`

`opacity()` takes one value from 0 to 1, or a percentage, and determines the image transparency based on it.

`0`, or `0%`, means totally transparent.
`1`, or `100%`, or higher, means totally visible.

Example:

```css
img {
  filter: opacity(0.5);
}
```

CSS also has an `opacity` property. `filter` however can be hardware accelerated, depending on the implementation, so this should be the preferred method.

### `drop-shadow()`

`drop-shadow()` shows a shadow behind the element, which follows the alpha channel. This means that if you have a transparent image, you get a shadow applied to the image shape, not the image box. If the image does not have an alpha channel, the shadow will be applied to the entire image box.

It accepts a minimum of 2 parameters, up to 5:

- *offset-x* sets the horizontal offset. Can be negative.
- *offset-y* sets the vertical offset. Can be negative.
- *blur-radius*, optional, sets the blur radius for the shadow. It defaults to 0, no blur.
- *spread-radius*, optional, sets the spread radius. Expressed in `px`, `rem` or `em`
- *color*, optional, sets the color of the shadow.

You can set the color without setting the spread radius or blur radius. CSS understands the value is a color and not a length value.

Example:

```css
img {
  filter: drop-shadow(10px 10px 5px orange);
}
```

```css
img {
  filter: drop-shadow(10px 10px orange);
}
```

```css
img {
  filter: drop-shadow(10px 10px 5px 5px #333);
}
```

### `grayscale()`

Make the element have a gray color.

You pass one value from 0 to 1, or from 0% to 100%, where 1 and 100% mean completely gray, and 0 or 0% mean the image is not touched, and the original colors remain.

Example:

```css
img {
  filter: grayscale(50%);
}
```

### `sepia()`

Make the element have a sepia color.

You pass one value from 0 to 1, or from 0% to 100%, where 1 and 100% mean completely sepia, and 0 or 0% mean the image is not touched, and the original colors remain.

Example:

```css
img {
  filter: sepia(50%);
}
```

### `invert()`

Invert the colors of an element. Inverting a color means looking up the opposite of a color in the HSL color wheel. Just search "color wheel" in Google if you have no idea what does that means. For example, the opposite of yellow is blue, the opposite of red is cyan. Every single color has an opposite.

You pass a number, from 0 to 1 or from 0% to 100%, that determines the amount of inversion. 1 or 100% means full inversion, 0 or 0% means no inversion.

0.5 or 50% will always render a 50% gray color, because you always end up in the middle of the wheel.

Example:

```css
img {
  filter: invert(50%);
}
```

### `hue-rotate()`

The HSL color wheel is represented in degrees. Using `hue-rotate()` you can rotate the color using a positive or negative rotation.

The function accepts a `deg` value.

Example:

```css
img {
  filter: hue-rotate(90deg);
}
```

### `brightness()`

Alters the brightness of an element.

0 or 0% gives a total black element.
1 or 100% gives an unchanged image

Values higher than 1 or 100% make the image brighter up to reaching a total white element.

Example:

```css
img {
  filter: brightness(50%);
}
```

### `contrast()`

Alters the contrast of an element.

0 or 0% gives a total gray element.
1 or 100% gives an unchanged image

Values higher than 1 or 100% give more contrast.

Example:

```css
img {
  filter: contrast(150%);
}
```

### `saturate()`

Alters the saturation of an element.

0 or 0% gives a total grayscale element (with less saturation).
1 or 100% gives an unchanged image

Values higher than 1 or 100% give more saturation.

Example:

```css
img {
  filter: saturate();
}
```

### `url()`

This filter allows to apply a filter defined in an SVG file. You point to the SVG file location.

Example:

```css
img {
  filter: url(filter.svg);
}
```

SVG filters are out of the scope of this book, but you can read more on this Smashing Magazine post: <https://www.smashingmagazine.com/2015/05/why-the-svg-filter-is-awesome/>