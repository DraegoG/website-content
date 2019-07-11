---
title: CSS Transforms
date: 2019-05-22T07:00:00+02:00
description: "How to work with the CSS `transform` property"
tags: css
---

Transforms allow you to translate, rotate, scale, and skew elements, in the 2D or 3D space. They are a very cool CSS feature, especially when combined with animations.

## 2D transforms

The `transform` property accepts those functions:

- `translate()` to move elements around
- `rotate()` to rotate elements
- `scale()` to scale elements in size
- `skew()` to twist or slant an element
- `matrix()` a way to perform any of the above operations using a matrix of 6 elements, a less user friendly syntax but less verbose

We also have axis-specific functions:

- `translateX()` to move elements around on the X axis
- `translateY()` to move elements around on the Y axis
- `scaleX()` to scale elements in size on the X axis
- `scaleY()` to scale elements in size on the Y axis
- `skewX()` to twist or slant an element on the X axis
- `skewY()` to twist or slant an element on the Y axis

Here is an example of a transform which changes the `.box` element width by 2 (duplicating it) and the height by 0.5 (reducing it to half):

```css
.box {
	transform: scale(2, 0.5);
}
```

[`transform-origin`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin) lets us set the origin (the `(0, 0)` coordinates) for the transformation, letting us change the rotation center.

## Combining multiple transforms

You can combine multiple transforms by separating each function with a space.

For example:

```css
transform: rotateY(20deg) scaleX(3) translateY(100px);
```

## 3D transforms

We can go one step further and move our elements in a 3D space instead than on a 2D space. With 3D, we are adding another axis, Z, which adds depth to out visuals.

Using the `perspective` property you can specify how far the 3D object is from the viewer.

Example:

```css
.3Delement {
  perspective: 100px;
}
```

`perspective-origin` determines the appearance of the position of the viewer, how are we looking at it in the X and Y axis.

Now we can use additional functions that control the Z axis, that adds up to the other X and Y axis transforms:

- `translateZ()`
- `rotateZ()`
- `scaleZ()`

and the corresponding shorthands `translate3d()`, `rotate3d()` and `scale3d()` as shorthands for using the `translateX()`, `translateY()` and `translateZ()` functions and so on.
