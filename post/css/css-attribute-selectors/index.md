---
title: CSS Attribute Selectors
date: 2019-04-29T07:00:00+02:00
description: "Learn how to use CSS attribute selectors"
tags: css
---

In this post I'll introduce attribute selectors.

> Also see [an introduction to the basic CSS Selectors](/css-selectors/). In there I introduce several of the basic CSS selectors: using element selectors, class, id, how to combine them, how to target multiple classes, how to style several selectors in the same rule, how to follow the page hierarchy with child and direct child selectors, and adjacent siblings.

## Attribute presence selectors

The first selector type is the attribute presence selector.

We can check if an element **has** an attribute using the `[]` syntax. `p[id]` will select all `p` tags in the page that have an `id` attribute, regardless of its value:

```css
p[id] {
  /* ... */
}
```

## Exact attribute value selectors

Inside the brackets you can check the attribute value using `=`, and the CSS will be applied only if the attribute matches the exact value specified:

```css
p[id="my-id"] {
  /* ... */
}
```

## Match an attribute value portion

While `=` let us check for exact value, we have other operators:

- `*=` checks if the attribute contains the partial
- `^=` checks if the attribute starts with the partial
- `$=` checks if the attribute ends with the partial
- `|=` checks if the attribute starts with the partial and it's followed by a dash (common in classes, for example), or just contains the partial
- `~=` checks if the partial is contained in the attribute, but separated by spaces from the rest

All the checks we mentioned are **case sensitive**.

If you add an `i` just before the closing bracket, the check will be case insensitive. It's supported in many browsers but not in all, check <https://caniuse.com/#feat=css-case-insensitive>.