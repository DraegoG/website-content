---
title: "How to get the value of an input element in React"
date: 2019-06-27T07:00:00+02:00
description: "Given a form, how do you get the value of one of the form fields?"
tags: react
---

A common scenario involves having a form, and you want to get the value of one of the form fields, for example when the user clicks a button.

How can you do so?

Using hooks, you can create a variable for each input field, and listening on the `onChange` event you call the "set" function for that variable.

Here's an example:

```js
const [title, setTitle] = useState('')
```

And on the input field in JSX:

```html
<input onChange={event => setTitle(event.target.value)} />
```

In this way, when you are in the event handler for the submit event of the form, or anywhere you want, you can get the value of the field from the `title` value.

