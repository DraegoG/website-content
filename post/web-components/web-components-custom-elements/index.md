---
title: "Web Components Custom Elements"
date: 2019-08-12T07:00:00+02:00
description: "An introductory tutorial to Custom Elements"
tags: web-components
---

> I wrote my first Custom Element using a CSS library called CSS Doodle. It's an amazing app that uses Custom Elements to let you create stunning CSS animations. That unlocked a whole new desire to figure out how that thing works under the hood. So I decided to take a better look at Web Components in general, a topic many people asked me to write about.

Custom Elements let us create new HTML tags.

I could not imagine why this could be a useful thing until I used that CSS Doodle library. After all we already have lots of tags.

> This tutorial covers Custom Elements version 1, the latest release of the standard at the time of writing

Using Custom Elements we can create a custom HTML tag with associated CSS and JavaScript.

It's not an alternative to frameworks like React, Angular or Vue, but it's a whole new concept.

The `window` global object exposes a `customElements` property that gives us access to a `CustomElementRegistry` object.

## The `CustomElementRegistry` object

This object has several methods we can use to register Custom Elements and query Custom Elements already registered:

- `define()` used to define a new Custom Element
- `get()` used to get the constructor of a Custom Element (returns `undefined` if not existing)
- `upgrade()` to upgrade a Custom Element
- `whenDefined()` used to get the constructor of a Custom Element. Similarly to `get()`, but it returns a promise instead, which resolves when the item is available.

## How to create a custom element

Before we can call the `window.customElements.define()` method, we must define a new HTML element by creating a new class that extends the HTMLElement built-in class:

```js
class CustomTitle extends HTMLElement {
	//...
}
```

Inside the class constructor we're going to use **Shadow DOM** to associate custom CSS, JavaScript and HTML to our new tag.

In this way, all we'll see in the HTML is our tag, but this will encapsulate a lot of functionality.

We start by initializing the constructor:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    //...
  }
}
```

Then, into it we call the `attachShadow()` method of the HTMLElement by passing an object with the `mode` property set to `'open'`. This property sets the encapsulation mode for the shadow DOM. If it's `open` we can access the `shadowRoot` property of an element. If it's closed, we can't.

Here's how to do so:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    //...
  }
}
```

Some examples you'll find use the syntax `const shadowRoot = this.attachShadow(/* ... */)` but you can avoid so unless you set `mode` to `closed`, as you can always reference that object by calling `this.shadowRoot`.

Which is what we're going to do now, to set the innerHTML of it:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    this.shadowRoot.innerHTML = `
      <h1>My Custom Title!</h1>
    `
  }
}
```

> You can add as many tags as you want, you're not limited to one tag inside the `innerHTML` property

Now we add this newly defined element to `window.customElements`:

```js
window.customElements.define('custom-title', CustomTitle)
```

and we can use the `<custom-title></custom-title>` Custom Element in the page!

> Note: you can't use self-closing tags (in other words: this `<custom-title />` is not allowed by the standard)

Notice the `-` dash in the tag name. **We are required to use a dash** in a Custom Element. This is how we can detect a built-in tag from a custom one.

Now we have this element in the page, and we can do what we do with other tags: target it with CSS and JavaScript!

## Provide a custom CSS for the element

In the constructor, you can pass a `style` tag in addition to the HTML tag that defines the content, and inside that you can have the Custom Element CSS:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    this.shadowRoot.innerHTML = `
      <style>
        h1 {
          font-size: 7rem;
          color: #000;
          font-family: Helvetica;
          text-align: center;
        }
      </style>
      <h1>My Custom Title!</h1>
    `
  }
}
```

Here's the example Custom Element we created, in Codepen:

<p class="codepen" data-height="446" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="LKgjzK" style="height: 446px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Web Components, My Custom Title">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/LKgjzK/">
  Web Components, My Custom Title</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## A shorter syntax

Instead of first defining the class and then calling
`window.customElements.define()` we can also use this shorthand syntax to define the class *inline*:

```js
window.customElements.define('custom-title', class extends HTMLElement {
  constructor() {
    ...
  }
})
```

## Add JavaScript

Just like we did for CSS, we can embed JavaScript.

We can't add it directly to the template tag like we did for CSS though.

Here I define a click event listener in the Custom Element constructor:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    this.shadowRoot.innerHTML = `
      <h1>My Custom Title!</h1>
    `
    this.addEventListener('click', e => {
      alert('clicked!')
    })
  }
}
```

## Alternative: use templates

Instead of defining the HTML and CSS in a JavaScript string, you can use a `template` tag in HTML and assign it an `id`:

```html
<template id="custom-title-template">
  <style>
    h1 {
      font-size: 7rem;
      color: #000;
      font-family: Helvetica;
      text-align: center;
    }
  </style>
  <h1>My Custom Title!</h1>
</template>

<custom-title></custom-title>
```

Then you can reference it in your Custom Element constructor and add it to the Shadow DOM:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    const tmpl = document.querySelector('#custom-title-template')
    this.shadowRoot.appendChild(tmpl.content.cloneNode(true))
  }
}

window.customElements.define('custom-title', CustomTitle)
```

Example on Codepen:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="oramEY" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Web Components, My Custom Title with template">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/oramEY/">
  Web Components, My Custom Title with template</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Lifecycle hooks

In addition to `constructor`, a Custom Element class can define those special methods that are executed at special times in the element lifecycle:

- `connectedCallback` when the element is inserted into the DOM
- `disconnectedCallback` when the element is removed from the DOM
- `attributeChangedCallback` when an *observed* attribute changed, or is added or removed
- `adoptedCallback` when the element has been [moved to a new document](https://developer.mozilla.org/en-US/docs/Web/API/Document/adoptNode)

```js
class CustomTitle extends HTMLElement {
  constructor() {
    ...
  }
  connectedCallback() {
    ...
  }
  disconnectedCallback() {
    ...
  }
  attributeChangedCallback(attrName, oldVal, newVal) {
    ...
  }
}
```

`attributeChangedCallback()` gets 3 parameters:

- the attribute name
- the old value of the attribute
- the new value of the attribute.

I mentioned it listens on observed attributes. What are those? We must define them in an array returned by the `observedAttributes` static method:

```js
class CustomTitle extends HTMLElement {
  constructor() {
    ...
  }

  static get observedAttributes() {
    return ['disabled']
  }

  attributeChangedCallback(attrName, oldVal, newVal) {
    ...
  }
}
```

I defined the `disabled` attribute to be observed.
Now when it changes, for example in JavaScript we set `disabled` to true:

```js
document.querySelector('custom-title').disabled = true
```

the `attributeChangedCallback()` fires with the set of parameters `'disabled', false, true`.

> Note: `attributeChangedCallback()` can be called on the element using JavaScript (for some unknown - to me - reason), but you shouldn't do that. It should just be invoked automatically by the browser

## Define custom attributes

You can define custom attributes for your Custom Elements by adding a getter and setter for them:

```js
class CustomTitle extends HTMLElement {
  static get observedAttributes() {
    return ['mycoolattribute']
  }

  get mycoolattribute() {
    return this.getAttribute('mycoolattribute')
  }

  set mycoolattribute(value) {
    this.setAttribute('mycoolattribute', value)
  }
}
```

This is how you can define boolean attributes, ones that are "true" if present, like `disabled` for HTML elements:

```js
class CustomTitle extends HTMLElement {
  static get observedAttributes() {
    return ['booleanattribute']
  }

  get booleanattribute() {
    return this.hasAttribute('booleanattribute')
  }

  set booleanattribute(value) {
    if (value) {
      this.setAttribute('booleanattribute', '')
    } else {
      this.removeAttribute('booleanattribute')
    }
  }
}
```

## How to style a Custom Element that's not yet defined

JavaScript might take a little to kick in and a Custom Element might not be defined as soon as the page loads. The page might do an ugly re-layout when the element is added in the page.

To solve this problem, add a `:not(:defined)` CSS pseudo class that sets the height and fades in the element when available:

```css
custom-title:not(:defined) {
 display: block;
 height: 400px;
 opacity: 0;
 transition: opacity 0.5s ease-in-out;
}
```

## Can I use them in all browsers?

The current versions of Firefox, Safari and Chrome support them. IE will never do, and Edge at the time of writing has support for them in development.

You can use this [polyfill](https://github.com/webcomponents/polyfills/tree/master/packages/custom-elements) to add a better support also for older browsers.

