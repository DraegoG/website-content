---
title: The CSS z-index property
date: 2019-07-25T07:00:00+02:00
description: "How to work with the `z-index` property in CSS"
tags: css
---

In the [positioning post](/css-positioning/) I mentioned that you can use the `z-index` property to control the Z axis positioning of elements.

It's very useful when you have multiple elements that overlap each other, and you need to decide which one is visible, as nearer to the user, and which one(s) should be hidden behind it.

This property takes a number (without decimals) and uses that number to calculate which elements appear nearer to the user, in the Z axis.

The higher the z-index value, the more an element is positioned nearer to the user.

When deciding which element should be visible and which one should be positioned behind it, the browser does a calculation on the z-index value.

The default value is `auto`, a special keyword. Using `auto`, the Z axis order is determined by the position of the HTML element in the page - the last sibling appears first, as it's defined last.

By default elements have the `static` value for the `position` property. In this case, the `z-index` property does not make any difference - it must be set to `absolute`, `relative` or `fixed` to work.

Example:

```css
.my-first-div {
	position: absolute;
	top: 0;
	left: 0;
	width: 600px;
	height: 600px;
	z-index: 10;
}

.my-second-div {
	position: absolute;
	top: 0;
	left: 0;
	width: 500px;
	height: 500px;
	z-index: 20;
}
```

The element with class `.my-second-div` will be displayed, and behind it `.my-first-div`.

Here we used 10 and 20, but you can use any number. Negative numbers too. It's common to pick non-consecutive numbers, so you can position elements in the middle. If you use consecutive numbers instead, you would need to re-calculate the z-index of each element involved in the positioning.