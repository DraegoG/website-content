---
title: CSS Media Queries and Responsive Design
date: 2019-05-19T07:00:00+02:00
description: "How to work with media queries in CSS to build responsive web pages"
tags: css
---

In this post I'm going to first introduce media types and media feature descriptors, then I'll explain media queries.

## Media types

Used in media queries and @import declarations, media types allow us to determine on which media a CSS file, or a piece of CSS, is loaded.

We have the following **media types**

- `all` means all the media
- `print` used when printing
- `screen` used when the page is presented on a screen
- `speech` used for screen readers

`screen` is the default.

In the past we had more of them, but most are deprecated as they proven to not be an effective way of determining device needs.

We can use them in @import statements like this:

```css
@import url(myfile.css) screen;
@import url(myfile-print.css) print;
```

We can load a CSS file on multiple media types separating each with a comma:

```css
@import url(myfile.css) screen, print;
```

The same works for the `link` tag in HTML:

```html
<link rel="stylesheet" type="text/css" href="myfile.css" media="screen" />
<link rel="stylesheet" type="text/css" href="another.css" media="screen, print" />
```

We're not limited to just using media types in the `media` attribute and in the `@import` declaration. There's more

## Media feature descriptors

First, let's introduce **media feature descriptors**. They are additional keywords that we can add to the `media` attribute of `link` or the the `@import` declaration, to express more conditionals over the loading of the CSS.

Here's the list of them:

- `width`
- `height`
- `device-width`
- `device-height`
- `aspect-ratio`
- `device-aspect-ratio`
- `color`
- `color-index`
- `monochrome`
- `resolution`
- `orientation`
- `scan`
- `grid`

Each of them have a corresponding min-* and max-*, for example:

- `min-width`, `max-width`
- `min-device-width`, `max-device-width`

and so on.

Some of those accept a length value which can be expressed in `px` or `rem` or any length value. It's the case of `width`, `height`, `device-width`, `device-height`.

For example:

```css
@import url(myfile.css) screen and (max-width: 800px);
```

Notice that we wrap each block using media feature descriptors in parentheses.

Some accept a fixed value. `orientation`, used to detect the device orientation, accepts `portrait` or `landscape`.

Example:

```css
<link rel="stylesheet" type="text/css" href="myfile.css" media="screen and (orientation: portrait)" />
```

`scan`, used to determine the type of screen, accepts `progressive` (for modern displays) or `interlace` (for older CRT devices)

Some others want an integer.

Like `color` which inspects the number of bits per color component used by the device. Very low-level, but you just need to know it's there for your usage (like `grid`, `color-index`, `monochrome`).

`aspect-ratio` and `device-aspect-ratio` accept a ratio value representing the width to height viewport ratio, which is expressed as a fraction.

Example:

```css
@import url(myfile.css) screen and (aspect-ratio: 4/3);
```

`resolution` represents the pixel density of the device, expressed in a [resolution data type](https://developer.mozilla.org/en-US/docs/Web/CSS/resolution) like `dpi`.

Example:

```css
@import url(myfile.css) screen and (min-resolution: 100dpi);
```

## Logic operators

We can combine rules using `and`:

```css
<link rel="stylesheet" type="text/css" href="myfile.css" media="screen and (max-width: 800px)" />
```

We can perform an "or" type of logic operation using commas, which combines multiple media queries:

```css
@import url(myfile.css) screen, print;
```

We can use `not` to negate a media query:

```css
@import url(myfile.css) not screen;
```

> Important: `not` can only be used to negate an entire media query, so it must be placed at the beginning of it (or after a comma)

## Media queries

All those above rules we saw applied to @import or the the `link` HTML tag can be applied inside the CSS, too.

You need to wrap them in a `@media () {}` structure.

Example:

```css
@media screen and (max-width: 800px) {
  /* enter some CSS */
}
```

and this is the foundation for **responsive design**.

Media queries can be quite complex. This example applies the CSS only if it's a screen device, the width is between 600 and 800 pixels, and the orientation is landscape:

```css
@media screen and (max-width: 800px) and (min-width: 600px) and (orientation: landscape) {
  /* enter some CSS */
}
```