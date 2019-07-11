---
title: "CSS Variables (Custom Properties)"
description: "Discover CSS Custom Properties, also called CSS Variables, a powerful new feature of modern browsers that help you write better CSS"
date: 2018-03-05T08:06:29+02:00
updated: 2018-05-16T08:06:29+02:00
tags: css
---

<!-- TOC -->

- [Introduction](#introduction)
- [The basics of using variables](#the-basics-of-using-variables)
- [Create variables inside any element](#create-variables-inside-any-element)
- [Variables scope](#variables-scope)
- [Interacting with a CSS Variable value using JavaScript](#interacting-with-a-css-variable-value-using-javascript)
- [Handling invalid values](#handling-invalid-values)
- [Browser support](#browser-support)
- [CSS Variables are case sensitive](#css-variables-are-case-sensitive)
- [Math in CSS Variables](#math-in-css-variables)
- [Media queries with CSS Variables](#media-queries-with-css-variables)
- [Setting a fallback value for var()](#setting-a-fallback-value-for-var)

<!-- /TOC -->

## Introduction

In the last few years CSS preprocessors had a lot of success. It was very common for greenfield projects to start with Less or Sass. And it's still a very popular technology.

The main benefits of those technologies are, in my opinion:

- They allow to nest selectors
- The provide an easy imports functionality
- They give you variables

Modern CSS has a new powerful feature called **CSS Custom Properties**, also commonly known as **CSS Variables**.

CSS is not a programming language like [JavaScript](https://flaviocopes.com/javascript/), Python, PHP, Ruby or Go where variables are key to do something useful. CSS is very limited in what it can do, and it's mainly a declarative syntax to tell browsers how they should display an HTML page.

But a variable is a variable: a name that refers to a value, and variables in CSS helps reduce repetition and inconsistencies in your CSS, by centralizing the values definition.

And it introduces a unique feature that CSS preprocessors won't never have: **you can access and change the value of a CSS Variable programmatically using JavaScript**.

## The basics of using variables

A CSS Variable is defined with a special syntax, prepending **two dashes** to a name (`--variable-name`), then a colon and a value. Like this:

```css
:root {
  --primary-color: yellow;
}
```

(more on `:root` later)

You can access the variable value using `var()`:

```css
p {
  color: var(--primary-color)
}
```

The variable value can be any valid CSS value, for example:

```css
:root {
  --default-padding: 30px 30px 20px 20px;
  --default-color: red;
  --default-background: #fff;
}
```

## Create variables inside any element

CSS Variables can be defined inside any element. Some examples:

```css
:root {
  --default-color: red;
}

body {
  --default-color: red;
}

main {
  --default-color: red;
}

p {
  --default-color: red;
}

span {
  --default-color: red;
}

a:hover {
  --default-color: red;
}
```

What changes in those different examples is the **scope**.

## Variables scope

Adding variables to a selector makes them available to all the children of it.

In the example above you saw the use of `:root` when defining a CSS variable:

```css
:root {
  --primary-color: yellow;
}
```

`:root` is a CSS pseudo-class that identifies the root element of a tree.

In the context of an HTML document, using the `:root` selector points to the `html` element, except that `:root` has higher [specificity](/css-specificity/) (takes priority).

In the context of an SVG image, `:root` points to the `svg` tag.

Adding a CSS custom property to `:root` makes it available to all the elements in the page.

If you add a variable inside a `.container` selector, it's only going to be available to children of `.container`:

```css
.container {
  --secondary-color: yellow;
}
```

and using it outside of this element is not going to work.

Variables can be **reassigned**:

```css
:root {
  --primary-color: yellow;
}

.container {
  --primary-color: blue;
}
```

Outside `.container`, `--primary-color` will be _yellow_, but inside it will be _blue_.

You can also assign or overwrite a variable inside the HTML using **inline styles**:

```html
<main style="--primary-color: orange;">
  <!-- ... -->
</main>
```

> CSS Variables follow the normal [CSS cascading rules](/css-cascade/), with precedence set according to [specificity](/css-specificity/)

## Interacting with a CSS Variable value using JavaScript

The coolest thing with CSS Variables is the ability to access and edit them using JavaScript.

Here's how you set a variable value using plain JavaScript:

```js
const element = document.getElementById('my-element')
element.style.setProperty('--variable-name', 'a-value')
```

This code below can be used to access a variable value instead, in case the variable is defined on `:root`:

```js
const styles = getComputedStyle(document.documentElement)
const value = String(styles.getPropertyValue('--variable-name')).trim()
```

Or, to get the style applied to a specific element, in case of variables set with a different scope:

```js
const element = document.getElementById('my-element')
const styles = getComputedStyle(element)
const value = String(styles.getPropertyValue('--variable-name')).trim()
```

## Handling invalid values

If a variable is assigned to a property which does not accept the variable value, it's considered invalid.

For example you might pass a pixel value to a `position` property, or a rem value to a color property.

In this case the line is considered invalid and ignored.

## Browser support

Browser support for CSS Variables is **very good**, [according to Can I Use](https://www.caniuse.com/#feat=css-variables).

CSS Variables are here to stay, and you can use them today if you don't need to support Internet Explorer and old versions of the other browsers.

If you need to support older browsers you can use libraries like [PostCSS](https://flaviocopes.com/postcss/) or [Myth](http://www.myth.io/), but you'll lose the ability to interact with variables via JavaScript or the Browser Developer Tools, as they are transpiled to good old variable-less CSS (and as such, you lose most of the power of CSS Variables).

## CSS Variables are case sensitive

This variable:

```css
--width: 100px;
```

is different than:

```css
--Width: 100px;
```

## Math in CSS Variables

To do math in CSS Variables, you need to use [`calc()`](/css-calc/), for example:

```css
:root {
  --default-left-padding: calc(10px * 2);
}
```

## Media queries with CSS Variables

Nothing special here. CSS Variables normally apply to media queries:

```css
body {
  --width: 500px;
}

@media screen and (max-width: 1000px) and (min-width: 700px) {
  --width: 800px;
}

.container {
  width: var(--width);
}
```

## Setting a fallback value for var()

`var()` accepts a second parameter, which is the default fallback value when the variable value is not set:

```css
.container {
  margin: var(--default-margin, 30px);
}
```