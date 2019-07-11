---
title: "Go Best Practices: Pointer or value receivers?"
date: 2017-08-06T11:04:59+02:00
tags: go
---

Common dilemma when defining the methods of a struct.

In particular when deciding your method receivers, should you use pointer receivers or value receivers?

```go
func (t *Type) Method() {} //pointer receiver
```

vs

```go
func (t Type) Method() {} //value receiver
```

Method receivers can be assimilated to function arguments in their behavior, and everything applicable to passing a pointer or a value as a function argument still applies for method receivers.

## When should you use pointer receivers

### Modify the receiver

If you want to change the state of the receiver in a method, manipulating the value of it, **use a pointer receiver**. It's not possible with a value receiver, which copies by value. Any modification to a value receiver is local to that copy.

### Optimization

If the struct you're defining the method on is very large, copying it would be far too expensive than using a value receiver.

Value receivers operate on a copy of the original type value. This means that there is a cost involved, especially if the struct is very large, and pointer received are more efficient.

## When value receivers are better

If you don't need to edit the receiver value, **use a value receiver**.

Value receivers are concurrency safe, while **pointer receivers are not concurrency safe**.

## When you should make a tradeoff

There is a situation when you might want to use pointer receivers for methods where you'd normally use a value receiver, and it's when you have other pointer receivers defined on that type, and for **consistency** you should use pointer receivers across all the methods.

## Read more

- [Should I define methods on values or pointers?](https://golang.org/doc/faq#methods_on_values_or_pointers)
- [Why do T and *T have different method sets?](https://golang.org/doc/faq#different_method_sets)