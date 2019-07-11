---
title: CSS Fonts
seotitle: The CSS Fonts Tutorial
date: 2019-06-26T07:00:00+02:00
description: "Learn how to work with fonts in CSS"
tags: css
---

At the dawn of the web you only had a handful of fonts you could choose from.

Thankfully today you can load any kind of font on your pages.

CSS has gained many nice capabilities over the years in regards to fonts.

The `font` property is the shorthand for a number of properties:

- `font-family`
- `font-weight`
- `font-stretch`
- `font-style`
- `font-size`

Let's see each one of them and then we'll cover `font`.

Then we'll talk about how to load custom fonts, using `@import` or `@font-face`, or by loading a font stylesheet.

## `font-family`

Sets the font _family_ that the element will use.

Why "family"? Because what we know as a font is actually composed of several sub-fonts. which provide all the style (bold, italic, light..) we need.

Here's an example from my Mac's Font Book app - the Fira Code font family hosts several dedicated fonts underneath:

![](Screen Shot 2019-04-09 at 07.28.20.png)

This property lets you select a specific font, for example:

```css
body {
  font-family: Helvetica;
}
```

You can set multiple values, so the second option will be used if the first cannot be used for some reason (if it's not found on the machine, or the network connection to download the font failed, for example):

```css
body {
  font-family: Helvetica, Arial;
}
```

I used some specific fonts up to now, ones we call **Web Safe Fonts**, as they are pre-installed on different operating systems.

We divide them in Serif, Sans-Serif, and Monospace fonts. Here's a list of some of the most popular ones:

**Serif**
- Georgia
- Palatino
- Times New Roman
- Times

**Sans-Serif**
- Arial
- Helvetica
- Verdana
- Geneva
- Tahoma
- Lucida Grande
- Impact
- Trebuchet MS
- Arial Black

**Monospace**
- Courier New
- Courier
- Lucida Console
- Monaco

You can use all of those as `font-family` properties, but they are not guaranteed to be there for every system. Others exist, too, with a varying level of support.

You can also use generic names:

- `sans-serif` a font without ligatures
- `serif` a font with ligatures
- `monospace` a font especially good for code
- `cursive` used to simulate handwritten pieces
- `fantasy` the name says it all

Those are typically used at the end of a `font-family` definition, to provide a fallback value in case nothing else can be applied:

```css
body {
  font-family: Helvetica, Arial, sans-serif;
}
```

## `font-weight`

This property sets the width of a font. You can use those predefined values:

* normal
* bold
* bolder (relative to the parent element)
* lighter (relative to the parent element)

Or using the numeric keywords

* 100
* 200
* 300
* 400, mapped to `normal`
* 500
* 600
* 700 mapped to `bold`
* 800
* 900

where 100 is the lightest font, and 900 is the boldest.

Some of those numeric values might not map to a font, because that must be provided in the font family. When one is missing, CSS makes that number be at least as bold as the preceding one, so you might have numbers that point to the same font.

## `font-stretch`

Allows to choose a narrow or wide face of the font, if available.

This is important: the font must be equipped with different faces.

Values allowed are, from narrower to wider:

- `ultra-condensed`
* `extra-condensed`
* `condensed`
* `semi-condensed`
* `normal`
* `semi-expanded`
* `expanded`
* `extra-expanded`
* `ultra-expanded`

## `font-style`

Allows you to apply an italic style to a font:

```css
p {
  font-style: italic;
}
```

This property also allows the values `oblique` and `normal`. There is very little, if any, difference between using `italic` and `oblique`. The first is easier to me, as HTML already offers an `i` element which means italic.

## `font-size`

This property is used to determine the size of fonts.

You can pass 2 kinds of values:

1. a length value, like `px`, `em`, `rem` etc, or a percentage
2. a predefined value keyword

In the second case, the values you can use are:

- xx-small
- x-small
- small
- medium
- large
- x-large
- xx-large
- smaller (relative to the parent element)
- larger (relative to the parent element)

Usage:

```css
p {
  font-size: 20px;
}

li {
  font-size: medium;
}
```

## `font-variant`

This property was originally used to change the text to small caps, and it had just 3 valid values:

- `normal`
- `inherit`
- `small-caps`

Small caps means the text is rendered in "smaller caps" beside its uppercase letters.

## `font`

The `font` property lets you apply different font properties in a single one, reducing the clutter.

We must at least set 2 properties, `font-size` and `font-family`, the others are optional:

```css
body {
  font: 20px Helvetica;
}
```

If we add other properties, they need to be put in the correct order.

This is the order:

```css
font: <font-stretch> <font-style> <font-variant> <font-weight> <font-size> <line-height> <font-family>;
```

Example:

```css
body {
  font: italic bold 20px Helvetica;
}

section {
  font: small-caps bold 20px Helvetica;
}
```

## Loading custom fonts using `@font-face`

`@font-face` lets you add a new font family name, and map it to a file that holds a font.

This font will be downloaded by the browser and used in the page, and it's been such a fundamental change to typography on the web - we can now use any font we want.

We can add `@font-face` declarations directly into our CSS, or link to a CSS dedicated to importing the font.

In our CSS file we can also use `@import` to load that CSS file.

A `@font-face` declaration contains several properties we use to define the font, including `src`, the URI (one or more URIs) to the font. This follows the same-origin policy, which means fonts can only be downloaded form the current origin (domain + port + protocol).

Fonts are usually in the formats

- `woff` (Web Open Font Format)
- `woff2` (Web Open Font Format 2.0)
- `eot` (Embedded Open Type)
- `otf` (OpenType Font)
- `ttf` (TrueType Font)

The following properties allow us to define the properties to the font we are going to load, as we saw above:

- `font-family`
- `font-weight`
- `font-style`
- `font-stretch`

## A note on performance

Of course loading a font has performance implications which you must consider when creating the design of your page.
