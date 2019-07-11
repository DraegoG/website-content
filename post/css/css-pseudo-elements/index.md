---
title: CSS Pseudo Elements
date: 2019-05-29T07:00:00+02:00
description: "Learn the basics of CSS Pseudo Elements"
tags: css
---

Pseudo-elements are used to style a specific part of an element.

They start with a double colon `::`.

> Sometimes you will spot them in the wild with a single colon, but this is only a syntax supported for backwards compatibility reasons. You should use 2 colons to distinguish them from pseudo-classes.

`::before` and `::after` are probably the most used pseudo-elements. They are used to add content before or after an element, like icons for example.

Here's the list of the pseudo-elements:

Pseudo-element | Targets
-------------|------------
`::after` | creates a pseudo-element after the element
`::before` | creates a pseudo-element before the element
`::first-letter` | can be used to style the first letter of a block of text
`::first-line` | can be used to style the first line of a block of text
`::selection` | targets the text selected by the user

Let's do an example. Say you want to make the first line of a paragraph slightly bigger in font size, a common thing in typography:

```css
p::first-line {
  font-size: 2rem;
}
```

Or maybe you want the first letter to be bolder:

```css
p::first-letter {
  font-weight: bolder;
}
```

`::after` and `::before` are a bit less intuitive. I remember using them when I had to add icons using CSS.

You specify the `content` property to insert any kind of content after or before an element:

```css
p::before {
  content: url(/myimage.png);
}

.myElement::before {
	content: "Hey Hey!";
}
```