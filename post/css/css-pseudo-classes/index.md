---
title: CSS Pseudo Classes
date: 2019-05-28T07:00:00+02:00
description: "Learn the basics of CSS Pseudo Classes"
tags: css
---

Pseudo classes are predefined keywords that are used to select an element based on its **state**, or to target a specific child.

They start with a **single colon** `:`.

They can be used as part of a selector, and they are very useful to style active or visited links for example, change the style on hover, focus, or target the first child, or odd rows. Very handy in many cases.

These are the most popular pseudo classes you will likely use:

Pseudo class | Targets
-------------|------------
`:active` | an element being activated by the user (e.g. clicked). Mostly used on links or buttons
`:checked` | a checkbox, option or radio input types that are enabled
`:default` | the default in a set of choices (like, option in a select or radio buttons)
`:disabled` | an element disabled
`:empty` | an element with no children
`:enabled` | an element that's enabled (opposite to `:disabled`)
`:first-child` | the first child of a group of siblings
`:focus` | the element with focus
`:hover` | an element hovered with the mouse
`:last-child` | the last child of a group of siblings
`:link` | a link that's not been visited
`:not()` | any element not matching the selector passed. E.g. `:not(span)`
`:nth-child()` | an element matching the specified position
`:nth-last-child()` | an element matching the specific position, starting from the end
`:only-child` | an element without any siblings
`:required` | a form element with the `required` attribute set
`:root` | represents the `html` element. It's like targeting `html`, but it's more specific. Useful in [CSS Variables](https://flaviocopes.com/css-variables/).
`:target` | the element matching the current URL fragment (for inner navigation in the page)
`:valid` | form elements that validated client-side successfully
`:visited` | a link that's been visited

Let's do an example. A common one, actually. You want to style a link, so you create a CSS rule to target the `a` element:

```css
a {
  color: yellow;
}
```

Things seem to work fine, until you click one link. The link goes back to the predefined color (blue) when you click it. Then when you open the link and go back to the page, now the link is blue.

Why does that happen?

Because the link when clicked changes state, and goes in the `:active` state. And when it's been visited, it is in the `:visited` state.  Forever, until the user clears the browsing history.

So, to correctly make the link yellow across all states, you need to write

```css
a,
a:visited,
a:active {
  color: yellow;
}
```

`:nth-child()` deserves a special mention. It can be used to target odd or even children with `:nth-child(odd)` and `:nth-child(even)`.

It is commonly used in lists to color odd lines differently from even lines:

```css
ul:nth-child(odd) {
  color: white;
	background-color: black;
}
```

You can also use it to target the first 3 children of an element with `:nth-child(-n+3)`. Or you can style 1 in every 5 elements with `:nth-child(5n)`.

Some pseudo classes are just used for printing, like `:first`, `:left`, `:right`, so you can target the first page, all the left pages, and all the right pages, which are usually styled slightly differently.