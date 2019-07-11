---
title: CSS Units
date: 2019-05-03T07:00:00+02:00
description: "Learn how to work with units in CSS"
tags: css
---

One of the things you'll use every day in CSS are **units**. They are used to set lengths, paddings, margins, align elements and so on.

Things like `px`, `em`, `rem`, or percentages.

They are everywhere. There are some relatively unknown ones, too.

## Pixels

The most widely used measurement unit. A pixel does not actually correlate to a physical pixel on your screen, as that varies, a lot, by device (think high-DPI devices vs non-retina devices).

There is a convention that make this unit work consistently across devices.

## Percentages

Another very useful measure, percentages let you specify values in percentages of that parent element's corresponding property.

Example:

```css
.parent {
  width: 400px;
}

.child {
  width: 50%; /* = 200px */
}
```

## Real-world measurement units

We have those measurement units which are translated from the outside world. Mostly useless on screen, they can be useful for print stylesheets. They are:

- `cm` a centimeter (maps to 37.8 pixels)
- `mm` a millimeter (0.1cm)
- `q` a quarter of a millimeter
- `in` an inch (maps to 96 pixels)
- `pt` a point (1 inch = 72 points)
- `pc` a pica (1 pica = 12 points)

## Relative units

- `em` is the value assigned to that element's `font-size`, therefore its exact value changes between elements. It does not change depending on the font used, just on the font size. In typography this measures the width of the `m` letter.
- `rem` is similar to `em`, but instead of varying on the current element font size, it uses the root element (`html`) font size. You set that font size once, and `rem` will be a consistent measure across all the page.
- `ex` is like `em`, but inserted of measuring the width of `m`, it measures the height of the `x` letter. It can change depending on the font used, and on the font size.
- `ch` is like `ex` but instead of measuring the height of `x` it measures the width of `0` (zero).

## Viewport units

- `vw` the **viewport width unit** represents a percentage of the viewport width. `50vw` means 50% of the viewport width.
- `vh` the **viewport height unit** represents a percentage of the viewport height. `50vh` means 50% of the viewport height.
- `vmin` the **viewport minimum unit** represents the minimum between the height or width in terms of percentage. `30vmin` is the 30% of the current width or height, depending which one is smaller
- `vmax` the **viewport maximum unit** represents the maximum between the height or width in terms of percentage. `30vmax` is the 30% of the current width or height, depending which one is bigger

## Fraction units

`fr` are fraction units, and they are used in [CSS Grid](/css-grid/) to divide space into fractions.
