---
title: "The CSS margin property"
date: 2018-03-10T09:06:15+02:00
description: "margin is a simple CSS property that has a shorthand syntax I keep forgetting about, so I wrote this reference post"
tags: css
---

The `margin` CSS property is commonly used in CSS to add space around an element.

Remember:

- `margin` adds space outside an element border
- `padding` adds space inside an element border

## Specific margin properties

`margin` has 4 related properties that alter the margin of a single edge at once:

- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

The usage of those is very simple and cannot be confused, for example:

```css
margin-left: 30px;
margin-right: 3em;
```

## Using the `margin` shorthand

`margin` is a shorthand to specify multiple margins at the same time, and depending on the number of values entered, it behaves differently.

### 1 value

Using a single value applies that to **all** the margins: top, right, bottom, left.

```css
margin: 20px;
```

### 2 values

Using 2 values applies the first to **bottom & top**, and the second to **left & right**.

```css
margin: 20px 10px;
```

### 3 values

Using 3 values applies the first to **top**, the second to **left & right**, the third to **bottom**.

```css
margin: 20px 10px 30px;
```

### 4 values

Using 4 values applies the first to **top**, the second to **right**, the third to **bottom**, the fourth to **left**.

```css
margin: 20px 10px 5px 0px;
```

So, the order is _top-right-bottom-left_.

## Values accepted

`margin` accepts values expressed in any kind of length unit, the most common ones are px, em, rem, but [many others exist](https://developer.mozilla.org/en-US/docs/Web/CSS/length).

It also accepts percentage values, and the special value `auto`.

## Using `auto` to center elements

`auto` can be used to tell the browser to select automatically a margin, and it's most commonly used to center an element in this way:

```
margin: 0 auto;
```

As said above, using 2 values applies the first to **bottom & top**, and the second to **left & right**.

The modern way to center elements is to use [Flexbox](https://flaviocopes.com/flexbox/), and its `justify-content: center;` directive.

Older browsers of course do not implement Flexbox, and if you need to support them `margin: 0 auto;` is still a good choice.

## Using a negative margin
`margin` is the only property related to sizing that can have a negative value. It's extremely useful, too.
Setting a negative top margin makes an element move over elements before it, and given enough negative value it will move out of the page.

A negative bottom margin moves up the elements after it.

A negative right margin makes the content of the element expand beyond its allowed content size.

A negative left margin moves the element left over the elements that precede it, and given enough negative value it will move out of the page.