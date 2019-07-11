---
title: CSS Feature Queries
date: 2019-05-20T07:00:00+02:00
description: "How to work with feature queries in CSS"
tags: css
---

Feature queries are a recent and relatively unknown ability of CSS, but a [well supported](https://caniuse.com/#feat=css-featurequeries) one.

We can use it to check if a feature is supported by the browser using the `@supports` keyword.

This is an example I think this is especially useful, at the time of writing, for checking if a browser supports CSS grid, which can be done using:

```css
@supports (display: grid) {
  /* apply this CSS */
}
```

We check if the browser supports the `grid` value for the `display` property.

We can use `@supports` for any CSS property, to check any value.

We can also use the logical operators `and`, `or` and `not` to build complex feature queries.

This example checks if the browser supports both [CSS Grid](/css-grid/) and [Flexbox](/flexbox/):


```css
@supports (display: grid) and (display: flex) {
  /* apply this CSS */
}
```