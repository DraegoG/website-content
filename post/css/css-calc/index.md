---
title: The CSS calc() function
date: 2019-06-07T07:00:00+02:00
description: "Learn how to work with the CSS calc() function"
tags: css
---

The `calc()` function lets you perform basic math operations on values, and it's especially useful when you need to add or subtract a length value from a percentage.

This is how it works:

```css
div {
	max-width: calc(80% - 100px)
}
```

It returns a length value, so it can be used anywhere you expect a pixel value.

You can perform

+ additions using `+`
+ subtractions using `-`
+ multiplication using `*`
+ division using `/`

> One caveat: with addition and subtraction, the space around the operator is mandatory, otherwise it does not work as expected.

Examples:

```css
div {
	max-width: calc(50% / 3)
}
```

```css
div {
	max-width: calc(50% + 3px)
}
```

