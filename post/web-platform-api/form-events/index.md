---
title: "Handling forms in JavaScript"
date: 2019-08-14T07:00:00+02:00
description: "Discover the basics of working with forms in HTML and JavaScript"
tags: browser
---

Forms are an extremely important part of HTML and the Web Platform. They allow users can interact with the page and

- search something on the site
- trigger filters to trim result pages
- send information

and much much more.

By default, forms submit their content to a server-side endpoint, which by default is the page URL itself:

```html
<form>
  ...
  <input type="submit">
</form>
```

We can override this behavior by setting the `action` attribute of the form element, using the HTML method defined by the `method` attribute, which defaults to `GET`:

```html
<form action="/contact" method="POST">
  ...
  <input type="submit">
</form>
```

Upon clicking the submit input element, the browser makes a POST request to the `/contact` URL on the same origin (protocol, domain and port).

Using JavaScript we can intercept this event, submit the form asynchronously (with [**XHR**](/xhr/) and [**Fetch**](/fetch-api/)), and we can also react to events happening on individual form elements.

## Intercepting a form submit event

I just described the default behavior of forms, without JavaScript.

In order to start working with forms with JavaScript you need to intercept the `submit` event on the form element:

```js
const form = document.querySelector('form')
form.addEventListener('submit', event => {
  // submit event detected
})
```

Now inside the submit event handler function we call the `event.preventDefault()` method to prevent the default behavior and avoid a form submit to reload the page:

```js
const form = document.querySelector('form')
form.addEventListener('submit', event => {
  // submit event detected
  event.preventDefault()
})
```

At this point clicking the submit event button in the form will not do anything, except giving us the control.

## Working with input element events

We have a number of events we can listen for in form elements

- `input` fired on form elements when the element value is changed
- `change` fired on form elements when the element value is changed. In the case of text `input` elements and `textarea`, it's fired only once when the element loses focus (not for every single character typed)
- `cut` fired when the user cuts text from the form element
- `copy` fired when the user copies text from the form element
- `paste` fired when the user pastes text into the form element
- `focus` fired when the form element gains focus
- `blur` fired when the form element loses focus

Here's a sample form demo on Codepen:

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="flaviocopes" data-slug-hash="zQrqNy" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Form events demo">
  <span>See the Pen <a href="https://codepen.io/flaviocopes/pen/zQrqNy/">
  Form events demo</a> by Flavio Copes (<a href="https://codepen.io/flaviocopes">@flaviocopes</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
