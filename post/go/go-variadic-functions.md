---
title: "Go Variadic Functions"
description: ""
date: 2017-05-01T11:04:59+02:00
tags: go
---

Variadic Functions are functions that accept an unlimited number of arguments. Typically, they are expressed in the form

```go
func hello(friends ...string) {
    // ...
}
```

Very easy to recognize from the 3 dots `...`.

We can call `hello()` like this:

```go
hello("tony", "mark", "mary", "joe")
```

or:

```go
hello("tony")
```

or with an infinite number of strings.

## An example from the standard library: `append()`

[`append`](https://golang.org/pkg/builtin/#append) is a variadic function, defined as

```go
func append(slice []Type, elems ...Type) []Type
```

A common usage is when removing an item at position `i` from an array `a`.

```go
a = append(a[:i], a[i+1:]...)
```

This line creates a new slice by removing the item at position `i` in `a`, by combining the items from 0 to i (not included), and from i+1 to the end.

What is the purpose of `...`?

`append` accepts a slice as first argument, and an unlimited number of arguments, all with a type [assignable](https://golang.org/ref/spec#Assignability) to the type of its elements.

Writing

```go
a = append(a[:i], a[i+1:]...)
```

is equivalent as writing

```go
a = append(a[:i], a[i+1], a[i+2], a[i+3], a[i+4]) //and so on, until the end of the slice.
```

Using `a[i+1:]...` is basically a shorthand syntax, as the Go spec describes in <https://golang.org/ref/spec#Passing_arguments_to_..._parameters>:

> If f is variadic with a final parameter p of type ...T, then within f the type of p is equivalent to type []T. If f is invoked with no actual arguments for p, the value passed to p is nil. Otherwise, the value passed is a new slice of type []T with a new underlying array whose successive elements are the actual arguments, which all must be assignable to T

[Playground](https://play.golang.org/p/cqeMkemn62)