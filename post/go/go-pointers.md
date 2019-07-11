---
title: "Go pointers in a nutshell"
date: 2016-10-05T11:04:59+02:00
tags: go
---

Pointers are not unique to Go, but Go has a unique flavour of pointers, so it’s good to learn why they are unique, as you’ll use pointers in every Go program.

## Why pointers?

Everything in Go is passed by value, as in C and in all languages descending from C.

If you pass an Int to a function, the variable is copied.

If you pass a pointer, the pointer is copied, but _not_ the value it points to.

So, in most cases pointers are used to call functions and pass parameters by reference.

## An example

Let’s take a simple variable `x`, defined as an integer with value `5`:

```go
x := 5
```

Now, the memory address of `x` can be obtained with `&x`

If you print `&x` with `fmt.Println`, you’ll see that it’s something like `0xc42000e248`: a memory address.

Now, we can assign this value to a variable, and that variable will be a pointer to `x`.

```go
y := &x
```

If we write this assignment statement

```go
*y = 10
```

the `x` value will now be `10`.

## No pointer arithmetic

Go pointers are similar to C and C++ pointers, but they are safer, as you cannot perform operations like

```go
var x *int;
x++;
```

on a pointer, because the address of a pointer cannot be altered. No pointer/array duality.

## Returning pointers of local function variables

Local function variables referenced by returned pointers will remain available while the pointer is available. This will make sure the pointer is always pointing to what you think.

## Nil pointers

The zero value of a pointer is `nil`. This means that a nil pointer is still possible, but this causes fewer issues than in other languages (C, Java, C++) because there are less types masked as pointers, and less other nils laying around. For example, strings in C are pointers. In Go, they are a type.

`nil` is not a common return for functions, like in single return value languages — error checking is more organized, and `nil` is not a common zero value. Many built-in data types (strings, arrays, maps, slices..) have zero values different than `nil`.

## References

- <https://dave.cheney.net/2014/03/17/pointers-in-go>

- <https://gopl.io/>