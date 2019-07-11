---
title: The Pug Guide
description: "How to use the Pug templating engine"
date: 2018-09-09T07:00:00+02:00
booktitle: "Pug"
tags: node
tags_weight: 50
path: pug
---

<!-- TOC -->

- [Introduction to Pug](#introduction-to-pug)
- [How does Pug look like](#how-does-pug-look-like)
- [Install Pug](#install-pug)
- [Setup Pug to be the template engine in Express](#setup-pug-to-be-the-template-engine-in-express)
- [Your first Pug template](#your-first-pug-template)
- [Interpolating variables in Pug](#interpolating-variables-in-pug)
- [Interpolate a function return value](#interpolate-a-function-return-value)
- [Adding id and class attributes to elements](#adding-id-and-class-attributes-to-elements)
- [Set the doctype](#set-the-doctype)
- [Meta tags](#meta-tags)
- [Adding scripts and styles](#adding-scripts-and-styles)
- [Inline scripts](#inline-scripts)
- [Loops](#loops)
- [Conditionals](#conditionals)
- [Set variables](#set-variables)
- [Incrementing variables](#incrementing-variables)
- [Assigning variables to element values](#assigning-variables-to-element-values)
- [Iterating over variables](#iterating-over-variables)
- [Including other Pug files](#including-other-pug-files)
- [Defining blocks](#defining-blocks)
- [Extending a base template](#extending-a-base-template)
- [Comments](#comments)
  - [Visible](#visible)
  - [Invisible](#invisible)

<!-- /TOC -->

## Introduction to Pug

What is Pug? It's a template engine for server-side Node.js applications.

Express is capable of handling server-side template engines. Template engines allow us to add data to a view, and generate HTML dynamically.

Pug is a new name for an old thing. It's _Jade 2.0_.

The name was changed from Jade to Pug due to a trademark issue in 2016, when the project released version 2. You can still use Jade, aka Pug 1.0, but going forward, it's best to use Pug 2.0

> Also see the [differences between Jade and Pug](https://pugjs.org/api/migration-v2.html)

Express uses Jade as the default. Jade is the old version of Pug, specifically Pug 1.0.

Although the last version of Jade is 3 years old (at the time of writing, summer 2018), it's still the default in Express for backward compatibility reasons.

In any new project, you should use Pug or another engine of your choice. The official site of Pug is <https://pugjs.org/>.

## How does Pug look like

```pug
p Hello from Flavio
```

This template will create a `p` tag with the content `Hello from Flavio`.

As you can see, Pug is quite special. It takes the tag name as the first thing in a line, and the rest is the content that goes inside it.

If you are used to template engines that use HTML and interpolate variables, like Handlebars (described next), you might run into issues, especially when you need to convert existing HTML to Pug. This online converter from HTML to Jade (which is very similar, but a little different than Pug) will be  a great help: <https://jsonformatter.org/html-to-jade>

## Install Pug

Installing Pug is as simple as running `npm install`:

```bash
npm install pug
```

## Setup Pug to be the template engine in Express

and when initializing the Express app, we need to set it:

```js
const path = require('path')
const express = require('express')
const app = express()
app.set('view engine', 'pug')
app.set('views', path.join(__dirname, 'views'))
```

## Your first Pug template

Create an about view:

```js
app.get('/about', (req, res) => {
  res.render('about')
})
```

and the template in `views/about.pug`:

```pug
p Hello from Flavio
```

This template will create a `p` tag with the content `Hello from Flavio`.

## Interpolating variables in Pug

You can interpolate a variable using

```js
app.get('/about', (req, res) => {
  res.render('about', { name: 'Flavio' })
})
```

```pug
p Hello from #{name}
```

## Interpolate a function return value

You can interpolate a function return value using

```js
app.get('/about', (req, res) => {
  res.render('about', { getName: () => 'Flavio' })
})
```

```pug
p Hello from #{getName()}
```

## Adding id and class attributes to elements

```pug
p#title
p.title
```

## Set the doctype

```pug
doctype html
```

## Meta tags

```pug
html
  head
    meta(charset='utf-8')
    meta(http-equiv='X-UA-Compatible', content='IE=edge')
    meta(name='description', content='Some description')
    meta(name='viewport', content='width=device-width, initial-scale=1')
```

## Adding scripts and styles

```pug
html
  head
    script(src="script.js")
    script(src='//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js')

    link(rel='stylesheet', href='css/main.css')
```

## Inline scripts

```pug
script alert('test')

script
  (function(b,o,i,l,e,r){b.GoogleAnalyticsObject=l;b[l]||(b[l]=
  function(){(b[l].q=b[l].q||[]).push(arguments)});b[l].l=+new Date;
  e=o.createElement(i);r=o.getElementsByTagName(i)[0];
  e.src='//www.google-analytics.com/analytics.js';
  r.parentNode.insertBefore(e,r)}(window,document,'script','ga'));
  ga('create','UA-XXXXX-X');ga('send','pageview');
```

## Loops

```pug
ul
  each color in ['Red', 'Yellow', 'Blue']
    li= color

ul
  each color, index in ['Red', 'Yellow', 'Blue']
    li= 'Color number ' + index + ': ' + color
```

## Conditionals

```pug
if name
  h2 Hello from #{name}
else
  h2 Hello
```

else-if works too:

```pug
if name
  h2 Hello from #{name}
else if anotherName
  h2 Hello from #{anotherName}
else
  h2 Hello
```

## Set variables

You can set variables in Pug templates:

```pug
- var name = 'Flavio'
- var age = 35
- var roger = { name: 'Roger' }
- var dogs = ['Roger', 'Syd']
```

## Incrementing variables

You can increment a numeric variable using `++`:

```pug
age++
```

## Assigning variables to element values

```pug
p= name
```

```pug
span.age= age
```

## Iterating over variables

You can use `for` or `each`. There is no difference.

```pug
for dog in dogs
    li= dog
```

```pug
ul
  each dog in dogs
    li= dog
```

You can use `.length` to get the number of items:

```pug
p There are #{values.length}
```

`while` is another kind of loop:

```pug
- var n = 0;

ul
  while n <= 5
    li= n++
```

## Including other Pug files

In a Pug file you can include other Pug files:

```pug
include otherfile.pug
```

## Defining blocks

A well organized template system will define a base template, and then all the other templates extend from it.

The way a part of a template can be extended is by using blocks:

```pug
html
  head
    script(src="script.js")
    script(src='//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js')

    link(rel='stylesheet', href='css/main.css')
    block head
  body
    block body
      h1 Home page
      p welcome
```

In this case one block, `body`, has some content, while `head` does not. `head` is intended to be used to add additional content to the heading, while the `body` content is made to be overridden by other pages.

## Extending a base template

A template can extend a base template by using the `extends` keyword:

```pug
extends home.pug
```

Once this is done, you need to redefine blocks. All the content of the template must go into blocks, otherwise the engine does not know where to put them.

Example:

```pug
extends home.pug

block body
  h1 Another page
  p Hey!
  ul
    li Something
    li Something else
```

You can redefine one or more blocks. The ones not redefined will be kept with the original template content.

## Comments

Comments in Pug can be of two types: visible or not visible in the resulting HTML.

### Visible

Inline:

```pug
// some comment
```

Block:

```pug
//
  some
  comment
```

### Invisible

Inline:

```pug
//- some comment
```

Block:

```pug
//-
  some
  comment
```
