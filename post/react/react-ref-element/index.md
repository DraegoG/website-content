---
title: How to reference a DOM element in React
date: 2018-12-08T07:00:00+02:00
description: "Find out how to ref a DOM element in React"
tags: react
---

React is great at abstracting away the DOM from you when building apps.

But what if you want to access the DOM element that a React component represents?

Maybe you have to add a library that interacts directly with the DOM like a chart library, maybe you need to call some DOM API, or add focus on an element.

> Whatever the reason is, a good practice is making sure there's no other way of doing so without accessing the DOM directly.

In the JSX of your component, you can assign the reference of the DOM element to a component property using this attribute:

```js
ref={el => this.someProperty = el}
```

Put this into context, for example with a `button` element:

```js
<button ref={el => (this.button = el)} />
```

`button` refers to a property of the component, which can then be used by the component's lifecycle methods (or other methods) to interact with the DOM:

```js
class SomeComponent extends Component {
  render() {
    return <button ref={el => (this.button = el)} />
  }
}
```

In a function component the mechanism is the same, you just avoid using `this` (since it does not point to the component instance) and use a property instead:

```js
function SomeComponent() {
  let button
  return <button ref={el => (button = el)} />
}
```
