---
title: "HTML forms"
seotitle: "How to use forms in HTML and all the form elements tags"
date: 2019-08-03T07:00:00+02:00
description: "Discover how to use forms in HTML and all the form elements tags"
tags: html
---

Forms are the way you can interact with a page, or an app, built with Web technologies.

You have a set of controls, and when you submit the form, either with a click to a "submit" button or programmatically, the browser will send the data to the server.

By default this data sending causes the page to reload after the data is sent, but using JavaScript you can alter this behavior (not going to explain how in this book).

A form is created using the `form` tag:

```html
<form>
	...
</form>
```

By default forms are submitted using the GET HTTP method. Which has its drawbacks, and usually you want to use POST.

You can set the form to use POST when submitted by using the `method` attribute:

```html
<form method="POST">
	...
</form>
```

The form is submitted, either using GET or POST, to the same URL where it resides.

So if the form is in the `https://flaviocopes.com/contacts` page, pressing the "submit" button will make a request to that same URL.

Which might result in nothing happening.

You need something server-side to handle the request, and typically you "listen" for those form submit events on a dedicated URL.

You can specify the URL via the `action` parameter:

```html
<form action="/new-contact" method="POST">
	...
</form>
```

This will cause the browser to submit the form data using POST to the `/new-contact` URL on the same origin.

If the origin (protocol + domain + port) is `https://flaviocopes.com` (port 80 is the default), this means the form data will be sent to `https://flaviocopes.com/new-contact `.

I talked about data. Which data?

Data is provided by users via the set of control that are available on the Web platform:

- input boxes (single line text)
- text areas (multiline text)
- select boxes (choose one option from a drop-down menu)
- radio buttons (choose one option from a list always visible)
- checkboxes (choose zero, one or more option)
- file uploads
- and more!

Let's introduce each one of them in the following form fields overview.

## The `input` tag
The `input` field is one of the most widely used form elements. It's also a very versatile element, and it can completely change behavior based on the `type` attribute.

The default behavior is to be a single-line text input control:

```html
<input />
```

Equivalent to using:

```html
<input type="text" />
```

As with all the other fields that follow, you need to give the field a name in order for its content to be sent to the server when the form is submitted:

```html
<input type="text" name="username" />
```

The `placeholder` attribute is used to have a text showing up, in light gray, when the field is empty. Useful to add a hint to the user of what to type:

```html
<input type="text" name="username" placeholder="Your username" />
```

### Email

Using `type="email"` will validate client-side (in the browser) an email for correctness (semantic correctness, not ensuring the email address is existing) before submitting.

```html
<input type="email" name="email" placeholder="Your email" />
```

### Password

Using `type="password"` will make every key entered appear as an asterisk (*) or dot, useful for fields that host a password.

```html
<input type="password" name="password" placeholder="Your password" />
```

### Numbers

You can have an input element accept only numbers:

```html
<input type="number" name="age" placeholder="Your age" />
```

You can specify a minimum and maximum value accepted:

```html
<input type="number" name="age" placeholder="Your age" min="18" max="110" />
```

The `step` attribute helps identify the steps between different values. For example this accepts a value between 10 and 50, at steps of 5:

```html
<input type="number" name="a-number"  min="10" max="50" step="5" />
```

### Hidden field

Fields can be hidden from the user. They will still be sent to the server upon the form submit:

```html
<input type="hidden" name="some-hidden-field" value="some-value" />
```

This is commonly used to store values like a CSRF token, used for security and user identification, or even to detect robots sending spam, using special techniques.

It can also just be used to identify a form and its action.

### Setting a default value

All those fields accept a predefined value. If the user does not change it, this will be the value sent to the server:

```html
<input type="number" name="age" value="18" />
```

If you set a placeholder, that value will appear if the user clears the input field value:

```html
<input type="number" name="age" placeholder="Your age" value="18" />
```

## Form submit

The `type="submit"` field is a button that, once pressed by the user, submits the form:

```html
<input type="submit">
```

The `value` attribute sets the text on the button, which if missing shows the "Submit" text:

```html
<input type="submit" value="Click me">
```

## Form validation

Browsers provide client-side validation functionality to forms.

You can set fields as required, ensuring they are filled, and enforce a specific format fo the input of each field.

Let's see both options.

### Set fields as required

The `required` attribute helps you with validation. If the field is not set, client-side validation fails and the browser does not submit the form:

```html
<input type="text" name="username" required />
```

### Enforce a specific format

I described the `type="email"` field above. It automatically validates the email address according to a format set in the specification.

In the `type="number"` field, I mentioned the `min` and `max` attribute to limit values entered to an interval.

You can do more.

You can enforce a specific format on any field.

The `pattern` attribute gives you the ability to set a regular expression to validate the value against.

I recommend reading my Regular Expressions Guide at [flaviocopes.com/javascript-regular-expressions/](https://flaviocopes.com/javascript-regular-expressions/).

 pattern="https://.*"

```html
<input type="text" name="username" pattern="[a-zA-Z]{8}" />
```

## Other fields

### File uploads

You can load files from your local computer and send them to the server using a `type="file"` input element:

```html
<input type="file" name="secret-documents">
```

You can attach multiple files:

```html
<input type="file" name="secret-documents" multiple>
```

You can specify one or more file types allowed using the `accept` attribute. This accepts images:

```html
<input type="file" name="secret-documents" accept="image/*">
```

You can use a specific MIME type, like `application/json` or set a file extension like `.pdf`. Or set multiple files extensions, like this:

```html
<input type="file" name="secret-documents" accept=".jpg, .jpeg, .png">
```

### Buttons

The `type="button"` input fields can be used to add additional buttons to the form, that are not submit buttons:

```html
<input type="button" value="Click me">
```

They are used to programmatically do something, using JavaScript.

There is a special field rendered as a button, whose special action is to clear the entire form and bring back the state of the fields to the initial one:

```html
<input type="reset">
```

### Radio buttons

Radio buttons are used to create a set of choices, of which one is pressed and all the others are disabled.

The name comes from old car radios that had this kind of interface.

You define a set of `type="radio"` inputs, all with the same `name` attribute, and different `value` attribute:

```html
<input type="radio" name="color" value="yellow">
<input type="radio" name="color" value="red">
<input type="radio" name="color" value="blue">
```

Once the form is submitted, the `color` data property will have one single value.

There's always one element checked. The first item is the one checked by default.

You can set the value that's pre-selected using the `checked` attribute. You can use it only once per radio inputs group.

### Checkboxes

Similar to radio boxes, but they allow multiple values to be chosen, or none at all.

You define a set of `type="checkbox"` inputs, all with the same `name` attribute, and different `value` attribute:

```html
<input type="checkbox" name="color" value="yellow">
<input type="checkbox" name="color" value="red">
<input type="checkbox" name="color" value="blue">
```

All those checkboxes will be unchecked by default. Use the `checked` attribute to enable them on page load.

Since this input field allows multiple values, upon form submit the value(s) will be sent to the server as an array.

### Date and time

We have a few input types to accept date values.

The `type="date"` input field allows the user to enter a date, and shows a date picker if needed:

```html
<input type="date" name="birthday">
```

The `type="time"` input field allows the user to enter a time, and shows a time picker if needed:

```html
<input type="time" name="time-to-pickup">
```

The `type="month"` input field allows the user to enter a month and a year:

```html
<input type="month" name="choose-release-month">
```

The `type="week"` input field allows the user to enter a week and a year:

```html
<input type="week" name="choose-week">
```

All those fields allow to limit the range and the step between each value. I recommend checking MDN for the little details on their usage.

The `type="datetime-local"` field lets you choose a date and a time.

```html
<input type="datetime-local" name="date-and-time">
```

Here is a page to test them all: [https://codepen.io/flaviocopes/pen/ZdWQPm](https://codepen.io/flaviocopes/pen/ZdWQPm)

### Color picker

You can let users pick a color using the `type="color"` element:

```html
<input type="color" name="car-color">
```

You set a default value using the `value` attribute:

```html
<input type="color" name="car-color" value="#000000">
```

The browser will take care of showing a color picker to the user.

### Range

This input element shows a slider element. People can use it to move from a starting value to an ending value:

```html
<input type="range" name="age" min="0" max="100" value="30">
```

You can provide an optional step:

```html
<input type="range" name="age" min="0" max="100" value="30" step="10">
```

### Telephone

The `type="tel"` input field is used to enter a phone number:

```html
<input type="tel" name="telephone-number">
```

The main selling point for using `tel` over `text` is on mobile, where the device can choose to show a numeric keyboard.

Specify a `pattern` attribute for additional validation:

```html
<input type="tel" pattern="[0-9]{3}-[0-9]{8}" name="telephone-number">
```

### URL

The `type="url"` field is used to enter a URL.

```html
<input type="url" name="website">
```

You can validate it using the `pattern` attribute:

```html
<input type="url" name="website"  pattern="https://.*">
```

## The `textarea` tag

The `textarea` element allows users to enter multi-line text. Compared to `input`, it requires an ending tag:

```html
<textarea></textarea>
```

You can set the dimensions using CSS, but also using the `rows` and `cols` attributes:

```html
<textarea rows="20" cols="10"></textarea>
```

As with the other form tags, the `name` attribute determines the name in the data sent to the server:

```html
<textarea name="article"></textarea>
```

## The `select` tag

This tag is used to create a drop-down menu.

The user can choose one of the options available.

Each option is created using the `option` tag. You add a name to the select, and a value to each option:

```html
<select name="color">
	<option value="red">Red</option>
	<option value="yellow">Yellow</option>
</select>
```

You can set an option disabled:

```html
<select name="color">
	<option value="red" disabled>Red</option>
	<option value="yellow">Yellow</option>
</select>
```

You can have one empty option:

```html
<select name="color">
	<option value="">None</option>
	<option value="red">Red</option>
	<option value="yellow">Yellow</option>
</select>
```

Options can be grouped using the `optgroup` tag. Each option group has a `label` attribute:

```html
<select name="color">
	<optgroup lavel="Primary">
		<option value="red">Red</option>
		<option value="yellow">Yellow</option>
		<option value="blue">Blue</option>
	</optgroup>
	<optgroup lavel="Others">
		<option value="green">Green</option>
		<option value="pink">Pink</option>
	</optgroup>
</select>
```
