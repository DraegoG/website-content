---
title: Introduction to CSS
date: 2018-05-23T07:07:09+02:00
updated: 2019-04-15T07:07:09+02:00
description: "CSS is the language that defines the visual appearance of an HTML page in the browser. It's evolving quickly, and thanks to the newest features, CSS has never been easier to use"
tags: css
---

<!-- TOC -->

- [What is CSS](#what-is-css)
- [A brief history of CSS](#a-brief-history-of-css)
- [How does CSS look like](#how-does-css-look-like)
- [Semicolons](#semicolons)
- [Formatting and indentation](#formatting-and-indentation)
- [How do you load CSS in a Web Page](#how-do-you-load-css-in-a-web-page)
  - [1: Using the `link` tag](#1-using-the-link-tag)
  - [2: using the `style` tag](#2-using-the-style-tag)
  - [3: inline styles](#3-inline-styles)

<!-- /TOC -->

## What is CSS

**CSS** (an abbreviation of **Cascading Style Sheets**) is the language that we use to style an HTML file, and tell the browser how should it render the elements on the page.

It was grown out of the necessity of styling web pages. Before CSS was introduced, people wanted a way to style their web pages, which looked all very similar and "academic" back in the day. You couldn't do much in terms of personalization.

HTML 3.2 introduced the option of defining colors inline as HTML element attributes, and presentational tags like `center` and `font`, but that escalated quickly into a far from ideal situation 😱.

CSS let us move everything presentation-related from the HTML to the CSS, so that HTML could get back being the format that defines the structure of the document, rather than how things should look in the browser.

CSS is continuously evolving, and CSS you used 5 years ago might just be outdated, as new idiomatic CSS techniques emerged and browsers changed.

## A brief history of CSS

Before moving on, I want to give you a brief recap of the history of CSS.

CSS was grown out of the necessity of styling web pages. Before CSS was introduced, people wanted a way to style their web pages, which looked all very similar and "academic" back in the day. You couldn't do much in terms of personalisation.

HTML 3.2 introduced the option of defining colors inline as HTML element attributes, and presentational tags like `center` and `font`, but that escalated quickly into a far from ideal situation.

CSS let us move everything presentation-related from the HTML to the CSS, so that HTML could get back being the format that defines the structure of the document, rather than how things should look in the browser.

CSS is continuously evolving, and CSS you used 5 years ago might just be outdated, as new idiomatic CSS techniques emerged and browsers changed.

It's hard to imagine the times when CSS was born and how different the web was.

At the time, we had several competing browsers, the main ones being Internet Explorer or Netscape Navigator.

Pages were styled by using HTML, with special presentational tags like `bold` and special attributes, most of which are now deprecated.

This meant you had a limited amount of customisation opportunities.

The bulk of the styling decisions were left to the browser.

Also, you built a site specifically for one of them, because each one introduced different non-standard tags to give more power and opportunities.

Soon people realised the need for a way to style pages, in a way that would work across all browsers.

After the initial idea proposed in 1994, CSS got its first release in 1996, when the CSS Level 1 ("CSS 1") recommendation was published.

CSS Level 2 ("CSS 2") got published in 1998.

Since then, work began on CSS Level 3. The CSS Working Group decided to split every feature and work on it separately, in modules.

Browsers weren't especially fast at implementing CSS. We had to wait until 2002 to have the first browser implement the full CSS specification: IE for Mac, as nicely described in this CSS Tricks post: <https://css-tricks.com/look-back-history-css/>

Internet Explorer implemented the box model incorrectly right from the start, which led to years of pain trying to have the same style applied consistently across browsers. We had to use various tricks and hacks to make browsers render things as we wanted.

Today things are much, much better. We can just use the CSS standards without thinking about quirks, most of the time, and CSS has never been more powerful.

We don't have official release numbers for CSS any more now, but the CSS Working Group releases a "snapshot" of the modules that are currently considered stable and ready to be included in browsers. This is the latest snapshot, from 2018: <https://www.w3.org/TR/css-2018/>

CSS Level 2 is still the base for the CSS we write today, and we have many more features built on top of it.

## How does CSS look like

A CSS **rule set** has one part called **selector**, and the other part called **declaration**. The declaration contains various **rules**, each composed by a **property**, and a **value**.

In this example, `p` is the selector, and applies one rule which sets the value `20px` to the `font-size` property:

```css
p {
  font-size: 20px;
}
```

Multiple rules are stacked one after the other:


```css
p {
  font-size: 20px;
}

a {
  color: blue;
}
```

A selector can target one or more items:

```js
p, a {
  font-size: 20px;
}
```

and it can target HTML tags, like above, or HTML elements that contain a certain class attribute with `.my-class`, or HTML elements that have a specific `id` attribute with `#my-id`.

More advanced selectors allow you to choose items whose attribute matches a specific value, or also items which respond to pseudo-classes (more on that later)


## Semicolons

Every CSS rule terminates with a semicolon. Semicolons are **not** optional, except after the last rule, but I suggest to always use them for consistency and to avoid errors if you add another property and forget to add the semicolon on the previous line.

## Formatting and indentation

There is no fixed rule for formatting. This CSS is valid:

```css
      p
      {
  font-size:           20px   ;
                      }

a{color:blue;}
```

but a pain to see. Stick to some conventions, like the ones you see in the examples above: stick selectors and the closing brackets to the left, indent 2 spaces for each rule, have the opening bracket on the same line of the selector, separated by one space.

Correct and consistent use of spacing and indentation is a visual aid in understanding your code.

## How do you load CSS in a Web Page

CSS can be loaded in a page in 3 ways: with a `style` tag in the page `head`, with an external CSS file, and inline in tags.
CSS is attached to an HTML page in different ways.

### 1: Using the `link` tag

The `link` tag is the way to include a CSS file. This is the preferred way to use CSS as it's intended to be used: one CSS file is included by all the pages of your site, and changing one line on that file affects the presentation of all the pages in the site.

To use this method, you add a `link` tag with the `href` attribute pointing to the CSS file you want to include. You add it inside the `head` tag of the site (not inside the `body` tag):

```html
<link rel="stylesheet" type="text/css" href="myfile.css">
```

The `rel` and `type` attributes are required too, as they tell the browser which kind of file we are linking to.

### 2: using the `style` tag

Instead of using the `link` tag to point to separate stylesheet containing our CSS, we can add the CSS directly inside a `style` tag. This is the syntax:

```html
<style>
...our CSS...
</style>
```

Using this method we can avoid creating a separate CSS file. I find this is a good way to experiment before "formalising" CSS to a separate file, or to add a special line of CSS just to a file.

### 3: inline styles

Inline styles are the third way to add CSS to a page. We can add a `style` attribute to any HTML tag, and add CSS into it.

```html
<div style="">...</div>
```

Example:

```html
<div style="background-color: yellow">...</div>
```
