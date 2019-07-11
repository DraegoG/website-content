---
title: CSS Typography
date: 2019-05-08T07:00:00+02:00
description: "How to work with typography in CSS"
tags: css
---

In this post I'll talk about styling text with CSS, using the following properties:

- `text-transform`
- `text-decoration`
- `text-align`
- `vertical-align`
- `line-height`
- `text-indent`
- `text-align-last`
- `word-spacing`
- `letter-spacing`
- `text-shadow`
- `white-space`
- `tab-size`
- `writing-mode`
- `hyphens`
- `text-orientation`
- `direction`
- `line-break`
- `word-break`
- `overflow-wrap`

## `text-transform`

This property can transform the case of an element.

There are 4 valid values:

- `capitalize` to uppercase the first letter of each word
- `uppercase` to uppercase all the text
- `lowercase` to lowercase all the text
- `none` to disable transforming the text, used to avoid inheriting the property

Example:

```css
p {
  text-transform: uppercase;
}
```

## `text-decoration`

This property is sed to add decorations to the text, including

- `underline`
- `overline`
- `line-through`
- `blink`
- `none`

Example:

```css
p {
  text-decoration: underline;
}
```

You can also set the style of the decoration, and the color.

Example:

```css
p {
  text-decoration: underline dashed yellow;
}
```

Valid style values are `solid`, `double`, `dotted`, `dashed`, `wavy`.

You can do all in one line, or use the specific properties:

- `text-decoration-line`
- `text-decoration-color`
- `text-decoration-style`

Example:

```css
p {
  text-decoration-line: underline;
  text-decoration-color: yellow;
  text-decoration-style: dashed;
}
```

## `text-align`

By default text align has the `start` value, meaning the text starts at the "start", origin 0, 0 of the box that contains it. This means top left in left-to-right languages, and top right in right-to-left languages.

Possible values are `start`, `end`, `left`, `right`, `center`, `justify` (nice to have a consistent spacing at the line ends):

```css
p {
  text-align: right;
}
```

## `vertical-align`

Determines how inline elements are vertically aligned.

We have several values for this property. First we can assign a length or percentage value. Those are used to align the text in a position higher or lower (using negative values) than the baseline of the parent element.

Then we have the keywords:

- `baseline` (the default), aligns the baseline to the baseline of the parent element
- `sub` makes an element subscripted, simulating the `sub` HTML element result
- `super` makes an element superscripted, simulating the `sup` HTML element result
- `top` align the top of the element to the top of the line
- `text-top` align the top of the element to the top of the parent element font
- `middle` align the middle of the element to the middle of the line of the parent
- `bottom` align the bottom of the element to the bottom of the line
- `text-bottom` align the bottom of the element to the bottom of the parent element font

## `line-height`

This allows you to change the height of a line. Each line of text has a certain font height, but then there is additional spacing vertically between the lines. That's the line height:

```css
p {
  line-height: 0.9rem;
}
```

## `text-indent`

Indent the first line of a paragraph by a set length, or a percentage of the paragraph width:

```css
p {
  text-indent: -10px;
}
```

## `text-align-last`

By default the last line of a paragraph is aligned following the `text-align` value. Use this property to change that behavior:

```css
p {
  text-align-last: right;
}
```

## `word-spacing`

Modifies the spacing between each word.

You can use the `normal` keyword, to reset inherited values, or use a length value:

```css
p {
  word-spacing: 2px;
}

span {
  word-spacing: -0.2em;
}
```

## `letter-spacing`

Modifies the spacing between each letter.

You can use the `normal` keyword, to reset inherited values, or use a length value:

```css
p {
  letter-spacing: 0.2px;
}

span {
  letter-spacing: -0.2em;
}
```

## `text-shadow`

Apply a shadow to the text. By default the text has now shadow.

This property accepts an optional color, and a set of values that set

- the X offset of the shadow from the text
- the Y offset of the shadow from the text
- the blur radius

If the color is not specified, the shadow will use the text color.

Examples:

```css
p {
  text-shadow: 0.2px 2px;
}

span {
  text-shadow: yellow 0.2px 2px 3px;
}
```

## `white-space`

Sets how CSS handles the white space, new lines and tabs inside an element.

Valid values that collapse white space are:

- `normal` collapses white space. Adds new lines when necessary as the text reaches the container end
- `nowrap` collapses white space. Does not add a new line when the text reaches the end of the container, and suppresses any line break added to the text
- `pre-line` collapses white space. Adds new lines when necessary as the text reaches the container end

Valid values that preserve white space are:

- `pre` preserves white space. Does not add a new line when the text reaches the end of the container, but preserves line break added to the text
- `pre-wrap` preserves white space. Adds new lines when necessary as the text reaches the container end

## `tab-size`

Sets the width of the tab character. By default it's 8, and you can set an integer value that sets the character spaces it takes, or a length value:

```css
p {
  tab-size: 2;
}

span {
  tab-size: 4px;
}
```

## `writing-mode`

Defines whether lines of text are laid out horizontally or vertically, and the direction in which blocks progress.

The values you can use are

- `horizontal-tb` (default)
- `vertical-rl` content is laid out vertically. New lines are put on the left of the previous
- `vertical-lr` content is laid out vertically. New lines are put on the right of the previous

## `hyphens`

Determines if hyphens should be automatically added when going to a new line.

Valid values are

- `none` (default)
- `manual` only add an hyphen when there is already a visible hyphen or a hidden hyphen (a special character)
- `auto` add hyphens when determined the text can have a hyphen.

## `text-orientation`

When `writing-mode` is in a vertical mode, determines the orientation of the text.

Valid values are

- `mixed` is the default, and if a language is vertical (like Japanese) it preserves that orientation, while rotating text written in western languages
- `upright` makes all text be vertically oriented
- `sideways` makes all text horizontally oriented

## `direction`

Sets the direction of the text. Valid values are `ltr` and `rtl`:

```css
p {
  direction: rtl;
}
```

## `word-break`

This property specifies how to break lines within words.

- `normal` (default) means the text is only broken between words, not inside a word
- `break-all` the browser can break a word (but no hyphens are added)
- `keep-all` suppress soft wrapping. Mostly used for CJK (Chinese/Japanese/Korean) text.

Speaking of CJK text, the property `line-break` is used to determine how text lines break. I'm not an expert with those languages, so I will avoid covering it.

## `overflow-wrap`

If a word is too long to fit a line, it can overflow outside of the container.

> This property is also known as `word-wrap`, although that is non-standard (but still works as an alias)

This is the default behavior (`overflow-wrap: normal;`).

We can use:

```css
p {
  overflow-wrap: break-word;
}
```

to break it at the exact length of the line, or

```css
p {
  overflow-wrap: anywhere;
}
```

if the browser sees there's a soft wrap opportunity somewhere earlier. No hyphens are added, in any case.

This property is very similar to `word-break`. We might want to choose this one on western languages, while `word-break` has special treatment for non-western languages.