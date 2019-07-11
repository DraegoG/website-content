---
title: Getting started with JSX
date: 2018-01-31T10:07:09+02:00
description: "JSX is a technology that was introduced by React. Let's dive into it"
booktitle: "JSX"
bookdescription: " "
tags: react
---

<!-- TOC -->

- [Introduction to JSX](#introduction-to-jsx)
- [A JSX primer](#a-jsx-primer)
- [Transpiling JSX](#transpiling-jsx)
- [JS in JSX](#js-in-jsx)
- [HTML in JSX](#html-in-jsx)
  - [You need to close all tags](#you-need-to-close-all-tags)
  - [camelCase is the new standard](#camelcase-is-the-new-standard)
  - [`class` becomes `className`](#class-becomes-classname)
  - [The style attribute changes its semantics](#the-style-attribute-changes-its-semantics)
  - [Forms](#forms)
- [CSS in React](#css-in-react)
  - [Why is this preferred over plain CSS / SASS / LESS?](#why-is-this-preferred-over-plain-css--sass--less)
  - [Is this the go-to solution?](#is-this-the-go-to-solution)
- [Forms in JSX](#forms-in-jsx)
  - [`value` and `defaultValue`](#value-and-defaultvalue)
  - [A more consistent onChange](#a-more-consistent-onchange)
- [JSX auto escapes](#jsx-auto-escapes)
- [White space in JSX](#white-space-in-jsx)
  - [Horizontal white space is trimmed to 1](#horizontal-white-space-is-trimmed-to-1)
  - [Vertical white space is eliminated](#vertical-white-space-is-eliminated)
- [Adding comments in JSX](#adding-comments-in-jsx)
- [Spread attributes](#spread-attributes)
- [How to loop in JSX](#how-to-loop-in-jsx)

<!-- /TOC -->

## Introduction to JSX

JSX is a technology that was introduced by React.

Although React can work completely fine without using JSX, it's an ideal technology to work with components, so React benefits a lot from JSX.

At first, you might think that using JSX is like mixing HTML and [JavaScript](https://flaviocopes.com/javascript/) (and as you'll see CSS).

But this is not true, because what you are really doing when using JSX syntax is writing a declarative syntax of what a component UI should be.

And you're describing that UI not using strings, but instead using JavaScript, which allows you to do many nice things.

## A JSX primer

Here is how you define a h1 tag containing a string:

```js
const element = <h1>Hello, world!</h1>
```

It looks like a strange mix of JavaScript and HTML, but in reality it's all JavaScript.

What looks like HTML, is actually  syntactic sugar for defining components and their positioning inside the markup.

Inside a JSX expression, attributes can be inserted very easily:

```js
const myId = 'test'
const element = <h1 id={myId}>Hello, world!</h1>
```

You just need to pay attention when an attribute has a dash (`-`) which is converted to camelCase syntax instead, and these 2 special cases:

- `class` becomes `className`
- `for` becomes `htmlFor`

because they are reserved words in JavaScript.

Here's a JSX snippet that wraps two components into a `div` tag:

```js
<div>
  <BlogPostsList />
  <Sidebar />
</div>
```

A tag always needs to be closed, because this is more XML than HTML (if you remember the XHTML days, this will be familiar, but since then the HTML5 loose syntax won). In this case a self-closing tag is used.

Notice how I wrapped the 2 components into a `div`. Why? Because **the render() function can only return a single node**, so in case you want to return 2 siblings, just add a parent. It can be any tag, not just `div`.

## Transpiling JSX

A browser cannot execute JavaScript files containing JSX code. They must be first transformed to regular JS.

How? By doing a process called **transpiling**.

We already said that JSX is optional, because to every JSX line, a corresponding plain JavaScript alternative is available, and that's what JSX is transpiled to.

For example the following two constructs are equivalent:

> Plain JS

```js
ReactDOM.render(
  React.createElement('div', { id: 'test' },
    React.createElement('h1', null, 'A title'),
    React.createElement('p', null, 'A paragraph')
  ),
  document.getElementById('myapp')
)
```

> JSX

```js
ReactDOM.render(
  <div id="test">
    <h1>A title</h1>
    <p>A paragraph</p>
  </div>,
  document.getElementById('myapp')
)
```

This very basic example is just the starting point, but you can already see how more complicated the plain JS syntax is compared to using JSX.

At the time of writing the most popular way to perform the **transpilation** is to use **Babel**, which is the default option when running `create-react-app`, so if you use it you don't have to worry, everything happens under the hood for you.

If you don't use `create-react-app` you need to setup Babel yourself.

## JS in JSX

JSX accepts any kind of JavaScript mixed into it.

Whenever you need to add some JS, just put it inside curly braces `{}`. For example here's how to use a constant value defined elsewhere:

```js
const paragraph = 'A paragraph'
ReactDOM.render(
  <div id="test">
    <h1>A title</h1>
    <p>{paragraph}</p>
  </div>,
  document.getElementById('myapp')
)
```

This is a basic example. Curly braces accept _any_ JS code:

```js
const paragraph = 'A paragraph'
ReactDOM.render(
  <table>
    {rows.map((row, i) => {
      return <tr>{row.text}</tr>
    })}
  </table>,
  document.getElementById('myapp')
)
```

As you can see _we nested JavaScript inside JSX defined inside JavaScript nested in JSX_. You can go as deep as you need.

## HTML in JSX

JSX resembles HTML a lot, but it's actually XML syntax.

In the end you render HTML, so you need to know a few differences between how you would define some things in HTML, and how you define them in JSX.

### You need to close all tags

Just like in XHTML, if you have ever used it, you need to close all tags: no more `<br>` but instead use the self-closing tag: `<br />` (the same goes for other tags)

### camelCase is the new standard

In HTML you'll find attributes without any case (e.g. `onchange`). In JSX, they are renamed to their camelCase equivalent:

- `onchange` => `onChange`
- `onclick` => `onClick`
- `onsubmit` => `onSubmit`

### `class` becomes `className`

Due to the fact that JSX is JavaScript, and `class` is a reserved word, you can't write

```js
<p class="description">
```

but you need to use

```js
<p className="description">
```

**The same applies to `for`** which is translated to `htmlFor`.

### The style attribute changes its semantics

The `style` attribute in HTML allows to specify inline style. In JSX it no longer accepts a string, and in [CSS in React](#css-in-react) you'll see why it's a very convenient change.

### Forms

Form fields definition and events are changed in JSX to provide more consistency and utility.

[Forms in JSX](#forms-in-jsx) goes into more details on forms.

## CSS in React

JSX provides a cool way to define CSS.

If you have a little experience with HTML inline styles, at first glance you'll find yourself pushed back 10 or 15 years, to a world where inline CSS was completely normal (nowadays it's demonized and usually just a "quick fix" go-to solution).

JSX style is not the same thing: first of all, instead of accepting a string containing CSS properties, the JSX `style` attribute only accepts an object. This means you define properties in an object:

```js
var divStyle = {
  color: 'white'
}

ReactDOM.render(<div style={divStyle}>Hello World!</div>, mountNode)
```

or

```js
ReactDOM.render(<div style={{ color: 'white' }}>Hello World!</div>, mountNode)
```

The CSS values you write in JSX are slightly different from plain CSS:

- the keys property names are camelCased
- values are just strings
- you separate each tuple with a comma

### Why is this preferred over plain CSS / SASS / LESS?

CSS is an **unsolved problem**. Since its inception, dozens of tools around it rose and then fell. The main problem with JS is that there is no scoping and it's easy to write CSS that is not enforced in any way, thus a "quick fix" can impact elements that should not be touched.

JSX allows components (defined in React for example) to completely encapsulate their style.

### Is this the go-to solution?

Inline styles in JSX are good until you need to

1. write media queries
2. style animations
3. reference pseudo classes (e.g. `:hover`)
4. reference pseudo elements (e.g. `::first-letter`)

In short, they cover the basics, but it's not the final solution.

## Forms in JSX

JSX adds some changes to how HTML forms work, with the goal of making things easier for the developer.

### `value` and `defaultValue`

The `value` attribute always holds the current value of the field.

The `defaultValue` attribute holds the default value that was set when the field was created.

_This helps solve some weird behavior of regular [DOM](https://flaviocopes.com/dom/) interaction when inspecting `input.value` and `input.getAttribute('value')` returning one the current value and one the original default value._

This also applies to the `textarea` field, e.g.

```html
<textarea>Some text</textarea>
```

but instead

```js
<textarea defaultValue={'Some text'} />
```

For `select` fields, instead of using

```js
<select>
  <option value="x" selected>
    ...
  </option>
</select>
```

use

```js
<select defaultValue="x">
  <option value="x">...</option>
</select>
```

### A more consistent onChange

Passing a function to the `onChange` attribute you can subscribe to events on form fields.

It works consistently across fields, even `radio`, `select` and `checkbox` input fields fire a `onChange` event.

`onChange` also fires when typing a character into an `input` or `textarea` field.

## JSX auto escapes

To mitigate the ever present risk of XSS exploits, JSX forces automatic escaping in expressions.

This means that you might run into issues when using an HTML entity in a string expression.

You expect the following to print `© 2019`:

```js
<p>{'&copy; 2019'}</p>
```

But it's not, it's printing `&copy; 2019` because the string is escaped.

To fix this you can either move the entities outside the expression:

```html
<p>&copy; 2019</p>
```

or by using a constant that prints the Unicode representation corresponding to the HTML entity you need to print:

```js
<p>{'\u00A9 2019'}</p>
```

## White space in JSX

To add white space in JSX there are 2 rules:

### Horizontal white space is trimmed to 1

If you have white space between elements in the same line, it's all trimmed to 1 white space.

```html
<p>Something       becomes               this</p>
```

becomes

```html
<p>Something becomes this</p>
```

### Vertical white space is eliminated

```html
<p>
  Something
  becomes
  this
</p>
```

becomes

```html
<p>Somethingbecomesthis</p>
```

To fix this problem you need to explicitly add white space, by adding a space expression like this:

```html
<p>
  Something
  {' '}becomes
  {' '}this
</p>
```

or by embedding the string in a space expression:

```html
<p>
  Something
  {' becomes '}
  this
</p>
```

## Adding comments in JSX

You can add comments to JSX by using the normal JavaScript comments inside an expression:

```js
<p>
  {/* a comment */}
  {
    //another comment
  }
</p>
```

## Spread attributes

In JSX a common operation is assigning values to attributes.

Instead of doing it manually, e.g.

```js
<div>
  <BlogPost title={data.title} date={data.date} />
</div>
```

you can pass

```js
<div>
  <BlogPost {...data} />
</div>
```

and the properties of the `data` object will be used as attributes automatically, thanks to the ES6 [**spread operator**](/javascript-spread-operator/).

## How to loop in JSX

If you have a set of elements you need to loop upon to generate a JSX partial, you can create a loop, and then add JSX to an array:

```js
const elements = [] //..some array

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<Element key={index} />)
}
```

Now when rendering the JSX you can embed the `items` array by wrapping it in curly braces:

```js
const elements = ['one', 'two', 'three'];

const items = []

for (const [index, value] of elements.entries()) {
  items.push(<li key={index}>{value}</li>)
}

return (
  <div>
    {items}
  </div>
)
```

You can do the same directly in the JSX, using `map` instead of a for-of loop:

```js
const elements = ['one', 'two', 'three'];
return (
  <ul>
    {elements.map((value, index) => {
      return <li key={index}>{value}</li>
    })}
  </ul>
)
```
