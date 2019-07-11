---
title: "React PropTypes"
date: 2018-11-02T07:00:00+02:00
description: "How to use PropTypes to set the required type of a prop"
tags: react
---

Since JavaScript is a dynamically typed language, we don't really have a way to enforce the type of a variable at compile time, and if we pass invalid types, they will fail at runtime or give weird results if the types are compatible but not what we expect.

Flow and [TypeScript](/typescript/) help a lot, but React has a way to directly help with props types, and even before running the code, our tools (editors, linters) can detect when we are passing the wrong values:

```js
import PropTypes from 'prop-types'
import React from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <div>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </div>
    )
  }
}

BlogPostExcerpt.propTypes = {
  title: PropTypes.string,
  description: PropTypes.string
}

export default BlogPostExcerpt
```

### Which types can we use

These are the fundamental types we can accept:

- PropTypes.array
- PropTypes.bool
- PropTypes.func
- PropTypes.number
- PropTypes.object
- PropTypes.string
- PropTypes.symbol

We can accept one of two types:

```js
PropTypes.oneOfType([
  PropTypes.string,
  PropTypes.number
]),
```

We can accept one of many values:

```js
PropTypes.oneOf(['Test1', 'Test2']),
```

We can accept an instance of a class:

```js
PropTypes.instanceOf(Something)
```

We can accept any React node:

```js
PropTypes.node
```

or even any type at all:

```js
PropTypes.any
```

Arrays have a special syntax that we can use to accept an array of a particular type:

```js
PropTypes.arrayOf(PropTypes.string)
```

Objects, we can compose an object properties by using

```js
PropTypes.shape({
  color: PropTypes.string,
  fontSize: PropTypes.number
})
```

### Requiring properties

Appending `isRequired` to any PropTypes option will cause React to return an error if that property is missing:

```js
PropTypes.arrayOf(PropTypes.string).isRequired,
PropTypes.string.isRequired,
```
