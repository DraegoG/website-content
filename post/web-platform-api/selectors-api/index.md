---
title: "The Selectors API: querySelector and querySelectorAll"
description: "Access DOM elements using querySelector and querySelectorAll. They accept any CSS selector, so you are no longer limited by selecting elements by `id`"
date: 2018-03-13T08:06:29+02:00
booktitle: The Selectors API
tags: browser
---

<!-- TOC -->

- [Introduction](#introduction)
- [The Selectors API](#the-selectors-api)
- [Basic jQuery to DOM API examples](#basic-jquery-to-dom-api-examples)
  - [Select by `id`](#select-by-id)
  - [Select by `class`](#select-by-class)
  - [Select by tag name](#select-by-tag-name)
- [More advanced jQuery to DOM API examples](#more-advanced-jquery-to-dom-api-examples)
  - [Select multiple items](#select-multiple-items)
  - [Select by HTML attribute value](#select-by-html-attribute-value)
  - [Select by CSS pseudo class](#select-by-css-pseudo-class)
  - [Select the descendants of an element](#select-the-descendants-of-an-element)

<!-- /TOC -->

## Introduction

jQuery and other [DOM](/dom/) libraries got a huge popularity boost in the past, among with other features they provided, thanks to an easy way to select elements on a page.

Traditionally browsers provided one single way to select a DOM element, and that was by its `id` attribute, with [`getElementById()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById), a method offered by the `document` object.

## The Selectors API

Since 2013 the [Selectors API](https://www.w3.org/TR/selectors-api/), the DOM allows you to use two more useful methods:

- `document.querySelector()`
- `document.querySelectorAll()`

> They can be safely used, [as caniuse.com tells us](https://caniuse.com/#feat=queryselector), and they are even fully supported on IE9 in addition to all the other modern browsers, so there is no reason to avoid them, unless you need to support IE8 (which has partial support) and below.

They accept any CSS selector, so you are no longer limited by selecting elements by `id`.

- `document.querySelector()` returns a single element, the first found
- `document.querySelectorAll()` returns all the elements, wrapped in a NodeList object.

Those are all valid selectors:

- `document.querySelector('#test')`
- `document.querySelector('.my-class')`
- `document.querySelector('#test .my-class')`
- `document.querySelector('a:hover')`

## Basic jQuery to DOM API examples

Here below is a translation of the popular jQuery API into native DOM API calls.

### Select by `id`

```js
$('#test')
document.querySelector('#test')
```

We use `querySelector` since an `id` is unique in the page

### Select by `class`

```js
$('.test')
document.querySelectorAll('.test')
```

### Select by tag name

```js
$('div')
document.querySelectorAll('div')
```

## More advanced jQuery to DOM API examples

### Select multiple items

```js
$('div, span')
document.querySelectorAll('div, span')
```

### Select by HTML attribute value

```js
$('[data-example="test"]')
document.querySelectorAll('[data-example="test"]')
```

### Select by CSS pseudo class

```js
$(':nth-child(4n)')
document.querySelectorAll(':nth-child(4n)')
```

### Select the descendants of an element

For example all `li` elements under `#test`:

```js
$('#test li')
document.querySelectorAll('#test li')
```