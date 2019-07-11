---
title: The CSS Display property
date: 2019-06-04T07:00:00+02:00
description: "How to work with the `display` property in CSS"
tags: css
---

The `display` property of an object determines how it is rendered by the browser.

It's a very important property, and probably the one with the highest number of values you can use.

Those values include:

- `block`
- `inline`
- `none`
- `contents`
- `flow`
- `flow-root`
- `table` (and all the `table-*` ones)
- `flex`
- `grid`
- `list-item`
- `inline-block`
- `inline-table`
- `inline-flex`
- `inline-grid`
- `inline-list-item`

plus others you will not likely use, like `ruby`.

Choosing any of those will considerably alter the behavior of the browser with the element and its children.

In this post I'll analyze the most important ones not covered elsewhere:

- `block`
- `inline`
- `inline-block`
- `none`

I cover others in separate posts:

- `table`  in the [Tables guide](/css-tables/)
- `flex` in the [Flexbox guide](/flexbox/)
- `grid` in the [CSS Grid guide](/css-grid/)


## `inline`

Inline is the default display value for every element in CSS.

All the HTML tags are displayed inline out of the box except some elements like `div`, `p` and `section`, which are set as `block` by the user agent (the browser).

Inline elements don't have any margin or padding applied.

Same for height and width.

You _can_ add them, but the appearance in the page won't change - they are calculated and applied automatically by the browser.

## `inline-block`

Similar to `inline`, but with `inline-block` `width` and `height` are applied as you specified.

## `block`

As mentioned, normally elements are displayed inline, with the exception of some elements, including

- `div`
- `p`
- `section`
- `ul`

which are set as `block` by the browser.

With `display: block`, elements are stacked one after each other, vertically, and every element takes up 100% of the page.

The values assigned to the `width` and `height` properties are respected, if you set them, along with `margin` and `padding`.

## `none`

Using `display: none` makes an element disappear. It's still there in the HTML, but just not visible in the browser.