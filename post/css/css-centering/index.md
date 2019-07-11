---
title: How to center an element with CSS
date: 2018-03-21T06:07:09+02:00
updated: 2019-04-27T15:07:09+02:00
description: "Centering an element with CSS has always been easy for some things, hard for others. Here is the full list of how to center with CSS, with modern CSS techniques as well"
tags: css
---

Centering an element in CSS is a task that is very different if you need to center horizontally or vertically.

In this post I explain the most common scenarios and how to solve them. If a new solution is provided by [Flexbox](https://flaviocopes.com/flexbox/) I ignore the old techniques because we need to move forward, and Flexbox is supported by browsers since years, IE10 included.

## Center horizontally

### Text

Text is very simple to center horizontally using the `text-align` property set to `center`:

```css
p {
  text-align: center;
}
```

### Blocks

The modern way to center anything that is not text is to use Flexbox:

```css
#mysection {
  display: flex;
  justify-content: center;
}
```

any element inside `#mysection` will be horizontally centered.

![Center horizontally](flexbox-horizontal-center.png)

---

Here is the alternative approach if you don't want to use Flexbox.

Anything that is not text can be centered by applying an automatic margin to left and right, and setting the width of the element:

```css
section {
  margin: 0 auto;
  width: 50%;
}
```

the above `margin: 0 auto;` is a shorthand for:

```css
section {
  margin-top: 0;
  margin-bottom: 0;
  margin-left: auto;
  margin-right: auto;
}
```

Remember to set the item to `display: block` if it's an inline element.

## Center vertically

Traditionally this has always been a difficult task. Flexbox now provides us a great way to do this in the simplest possible way:

```css
#mysection {
  display: flex;
  align-items: center;
}
```

any element inside `#mysection` will be vertically centered.

![Center vertically](flexbox-vertical-center.png)

## Center both vertically and horizontally

Flexbox techniques to center vertically and horizontally can be combined to completely center an element in the page.

```css
#mysection {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

![Center both vertically and horizontally](flexbox-center.png)

The same can be done using [CSS Grid](https://flaviocopes.com/css-grid/):

```css
body {
  display: grid;
  place-items: center;
  height: 100vh;
}
```