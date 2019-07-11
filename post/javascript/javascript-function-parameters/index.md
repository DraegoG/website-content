---
title: JavaScript Function Parameters
date: 2019-06-06T07:00:00+02:00
description: "Learn the basics of JavaScript Function Parameters"
tags: js
---

A function can accept one or more parameters.

```js
const dosomething = () => {
  //do something
}

const dosomethingElse = foo => {
  //do something
}

const dosomethingElseAgain = (foo, bar) => {
  //do something
}
```

Starting with [ES6/ES2015](/es6/), functions can have default values for the parameters:

```js
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}
```

This allows you to call a function without filling all the parameters:

```js
dosomething(3)
dosomething()
```

[ES2018](/es2018/) introduced trailing commas for parameters, a feature that helps reducing bugs due to missing commas when moving around parameters (e.g. moving the last in the middle):

```js
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}

dosomething(2, 'ho!')
```

You can wrap all your arguments in an array, and use the [**spread operator**](/javascript-spread-operator/) when calling the function:

```js
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}
const args = [2, 'ho!']
dosomething(...args)
```

With many parameters, remembering the order can be difficult. Using objects, destructuring allows to keep the parameter names:

```js
const dosomething = ({ foo = 1, bar = 'hey' }) => {
  //do something
  console.log(foo) // 2
  console.log(bar) // 'ho!'
}
const args = { foo: 2, bar: 'ho!' }
dosomething(args)
```


Functions now support default parameters:

```js
const foo = function(index = 0, testing = true) { /* ... */ }
foo()
```

Default parameter values have been introduced in ES2015, and are widely implemented in modern browsers.

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

With object destructuring you can provide default values, which simplifies the code a lot:

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
