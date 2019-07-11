---
title: Styled Components
date: 2018-02-08T10:04:59+02:00
description: "Styled Components are one of the new ways to use CSS in modern JavaScript. It is the meant to be a successor of CSS Modules, a way to write CSS that's scoped to a single component, and not leak to any other element in the page"
tags: react
---

<!-- TOC -->

- [A brief history](#a-brief-history)
- [Introducing Styled Components](#introducing-styled-components)
- [Installation](#installation)
- [Your first styled component](#your-first-styled-component)
- [Using props to customize components](#using-props-to-customize-components)
- [Extending an existing Styled Component](#extending-an-existing-styled-component)
- [It's Regular CSS](#its-regular-css)
- [Using Vendor Prefixes](#using-vendor-prefixes)
- [Conclusion](#conclusion)

<!-- /TOC -->

## A brief history

Once upon a time, the Web was really simple and CSS didn't even exist. We laid out pages using **tables** and frames. Good times.

Then **CSS** came to life, and after some time it became clear that frameworks could greatly help especially in building grids and layouts, Bootstrap and Foundation playing a big part in this.

Preprocessors like **SASS** and others helped a lot to slow down the adoption of frameworks, and to better organize the code, conventions like **BEM** and **SMACSS** grew in use, especially within teams.

Conventions are not a solution to everything, and they are complex to remember, so in the last few years with the increasing adoption of [JavaScript](https://flaviocopes.com/javascript/) and build processes in every frontend project, CSS found its way into JavaScript (**CSS-in-JS**).

New tools explored new ways of doing CSS-in-JS and a few succeeded with increasing popularity:

- React Style
- jsxstyle
- Radium

and more.

## Introducing Styled Components

One of the most popular of these tools is **Styled Components**.

It is the meant to be a successor to **CSS Modules**, a way to write CSS that's scoped to a single component, and not leak to any other element in the page.

(more on CSS modules [here](https://css-tricks.com/css-modules-part-1-need/) and [here](https://glenmaddern.com/articles/css-modules))

Styled Components allow you to write plain CSS in your components without worrying about class name collisions.

## Installation

Install styled-components using [npm](https://flaviocopes.com/npm/) or [yarn](https://flaviocopes.com/yarn/):

```bash
npm install styled-components
yarn add styled-components
```

That's it! Now all you have to do is to add this import:

```js
import styled from 'styled-components'
```

## Your first styled component

With the `styled` object imported, you can now start creating Styled Components. Here's the first one:

```js
const Button = styled.button`
  font-size: 1.5em;
  background-color: black;
  color: white;
`
```

`Button` is now a [React](https://flaviocopes.com/react/) Component in all its greatness.

We created it using a function of the styled object, called `button` in this case, and passing some CSS properties in a [template literal](https://flaviocopes.com/javascript-template-literals/).

Now this component can be rendered in our container using the normal React syntax:

```js
render(<Button />)
```

Styled Components offer other functions you can use to create other components, not just `button`, like `section`, `h1`, `input` and many others.

The syntax used, with the backtick, might be weird at first, but it's called [Tagged Templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals), it's plain JavaScript and it's a way to pass an argument to the function.

## Using props to customize components

When you pass some props to a Styled Component, it will pass them down to the [DOM](https://flaviocopes.com/dom/) node mounted.

For example here's how we pass the `placeholder` and `type` props to an `input` component:

```js
const Input = styled.input`
  //...
`

render(
  <div>
    <Input placeholder="..." type="text" />
  </div>
)
```

This will do just what you think, inserting those props as HTML attributes.

Props instead of just being blindly passed down to the [DOM](https://flaviocopes.com/dom/) can also be used to customize a component based on the prop value. Here's an example:

```js
const Button = styled.button`
  background: ${props => (props.primary ? 'black' : 'white')};
  color: ${props => (props.primary ? 'white' : 'black')};
`

render(
  <div>
    <Button>A normal button</Button>
    <Button>A normal button</Button>
    <Button primary>The primary button</Button>
  </div>
)
```

Setting the `primary` prop changes the color of the button.

## Extending an existing Styled Component

If you have one component and you want to create a similar one, just styled slightly differently, you can use `extend`:

```js
const Button = styled.button`
  color: black;
  //...
`

const WhiteButton = Button.extend`
  color: white;
`

render(
  <div>
    <Button>A black button, like all buttons</Button>
    <WhiteButton>A white button</WhiteButton>
  </div>
)
```

## It's Regular CSS

In Styled Components, you can use the CSS you already know and love. It's just plain CSS. It is not pseudo CSS nor inline CSS with its limitations.

You can use media queries, [nesting](https://tabatkins.github.io/specs/css-nesting/) and anything else you might need.

## Using Vendor Prefixes

Styled Components automatically add all the vendor prefixes needed, so you don't need to worry about this problem.

## Conclusion

That's it for this Styled Components introduction! These concepts will help you get an understanding of the concept and help you get up and running with this way of using CSS in JavaScript.
