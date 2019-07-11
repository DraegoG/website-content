---
title: "Go Best Practices: Should you use a method or a function?"
date: 2017-08-06T11:04:59+02:00
tags: go
---

One of the key decisions when building a Go program, among many others, is **how to organize the program functionality**.

In particular, in this article I'm going to explain **when you should use a method, and when you should use a function**.

The two options are quite similar in their definition. The only difference is that a method is attached to a type:

```go
// function
func something(s string) {}

//methods
func (MyType) something(s string) {}
func (*MyType) something(s string) {}
```

If you come from an object oriented language like Ruby, Python or modern PHP, you might be tempted to build all your code around types and methods, as that's how those languages force you to think. There is nothing outside objects and methods.

If you come from a [JavaScript](/javascript/) background you might think of methods as the object prototype methods, which I think is a good comparison if you come from good old pre-classes JavaScript, while functions are just functions.

## It's a matter of state

Functions do not depend on state in any way.

As per the mathematical definition a function, provided some input parameters, the output values will always be the same.

Methods on the other way are tightly linked to the type on which they are attached, as they define its behavior, and use its value.

They get some value out of the type they're defined against, and if they have pointer receivers, they manipulate its state.

If your methods are not depending on the state, they should probably be defined as functions.

## Credits

Inspired by Steve Francia's talk "7 Common mistakes in Go and how to avoid them":

<iframe src="https://player.vimeo.com/video/115776445?byline=0&portrait=0" width="100%" height="500" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
