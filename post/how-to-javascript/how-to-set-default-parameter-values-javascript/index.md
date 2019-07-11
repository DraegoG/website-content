---
title: "How to set default parameter values in JavaScript"
date: 2018-12-05T07:00:00+02:00
description: "Find out how to add a default parameter value into a JavaScript function"
tags: js
---

Default parameter values have been introduced in [ES6](/es6/) in 2015, and are widely implemented in modern browsers.

This is a `doSomething` function which accepts `param1`.

```js
const doSomething = (param1) => {

}
```

We can add a default value for `param1` if the function is invoked without specifying a parameter:

```js
const doSomething = (param1 = 'test') => {

}
```

This works for more parameters as well, of course:

```js
const doSomething = (param1 = 'test', param2 = 'test2') => {

}
```

What if you have an unique object with parameters values in it?

Once upon a time, if we had to pass an object of options to a function, in order to have default values of those options if one of them was not defined, you had to add a little bit of code inside the function:

```js
const colorize = (options) => {
  if (!options) {
    options = {}
  }

  const color = ('color' in options) ? options.color : 'yellow'
  ...
}
```

With destructuring you can provide default values, which simplifies the code a lot:

```js
const colorize = ({ color = 'yellow' }) => {
  ...
}
```

If no object is passed when calling our `colorize` function, similarly we can assign an empty object by default:

```js
const spin = ({ color = 'yellow' } = {}) => {
  ...
}
```
