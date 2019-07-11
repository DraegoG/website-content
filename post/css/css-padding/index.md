---
title: CSS Padding
seotitle: The CSS Padding Tutorial
date: 2019-06-28T07:00:00+02:00
description: "How to work with padding in CSS"
tags: css
---

The `padding` CSS property is commonly used in CSS to add space in the inner side of an element.

Remember:

- `margin` adds space outside an element border
- `padding` adds space inside an element border

## Specific padding properties

`padding` has 4 related properties that alter the padding of a single edge at once:

- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`

The usage of those is very simple and cannot be confused, for example:

```css
padding-left: 30px;
padding-right: 3em;
```

## Using the `padding` shorthand

`padding` is a shorthand to specify multiple padding values at the same time, and depending on the number of values entered, it behaves differently.

### 1 value

Using a single value applies that to **all** the paddings: top, right, bottom, left.

```css
padding: 20px;
```

### 2 values

Using 2 values applies the first to **bottom & top**, and the second to **left & right**.

```css
padding: 20px 10px;
```

### 3 values

Using 3 values applies the first to **top**, the second to **left & right**, the third to **bottom**.

```css
padding: 20px 10px 30px;
```

### 4 values

Using 4 values applies the first to **top**, the second to **right**, the third to **bottom**, the fourth to **left**.

```css
padding: 20px 10px 5px 0px;
```

So, the order is _top-right-bottom-left_.

## Values accepted

`padding ` accepts values expressed in any kind of length unit, the most common ones are px, em, rem, but [many others exist](https://developer.mozilla.org/en-US/docs/Web/CSS/length).
