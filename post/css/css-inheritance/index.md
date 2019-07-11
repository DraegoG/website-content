---
title: CSS Inheritance
date: 2019-05-27T07:00:00+02:00
description: "Learn what CSS Inheritance means and why it's important"
tags: css
---

When you set some properties on a selector in CSS, they are inherited by all the children of that selector.

I said *some*, because not all properties show this behaviour.

This happens because some properties make sense to be inherited. This helps us write CSS much more concisely, since we don't have to explicitly set that property again on every single children.

Some other properties make more sense to *not* be inherited.

Think about fonts: you don't need to apply the `font-family` to every single tag of your page. You set the `body` tag font, and every children inherits it, along with other properties.

The `background-color` property, on the other hand, makes little sense to be inherited.

## Properties that inherit

Here is a list of the properties that do inherit. The list is non-comprehensive, but those rules are just the most popular ones you'll likely use:

- `border-collapse`
- `border-spacing`
- `caption-side`
- `color`
- `cursor`
- `direction`
- `empty-cells`
- `font-family`
- `font-size`
- `font-style`
- `font-variant`
- `font-weight`
- `font-size-adjust`
- `font-stretch`
- `font`
- `letter-spacing`
- `line-height`
- `list-style-image`
- `list-style-position`
- `list-style-type`
- `list-style`
- `orphans`
- `quotes`
- `tab-size`
- `text-align`
- `text-align-last`
- `text-decoration-color`
- `text-indent`
- `text-justify`
- `text-shadow`
- `text-transform`
- `visibility`
- `white-space`
- `widows`
- `word-break`
- `word-spacing`

I got it from this [nice Sitepoint article](https://www.sitepoint.com/css-inheritance-introduction/) on CSS inheritance.

## Forcing properties to inherit

What if you have a property that's not inherited by default, and you want it to, in a children?

In the children, you set the property value to the special keyword `inherit`.

Example:

```css
body {
	background-color: yellow;
}

p {
  background-color: inherit;
}
```

## Forcing properties to NOT inherit

On the contrary, you might have a property inherited and you want to avoid so.

You can use the `revert` keyword to revert it. In this case, the value is reverted to the original value the browser gave it in its default stylesheet.

In practice this is rarely used, and most of the times you'll just set another value for the property to overwrite that inherited value.

## Other special values
In addition to the `inherit` and `revert` special keywords we just saw, you can also set any property to:

- `initial`: use the default browser stylesheet if available. If not, and if the property inherits by default, inherit the value. Otherwise do nothing.
- `unset`: if the property inherits by default, inherit. Otherwise do nothing.
