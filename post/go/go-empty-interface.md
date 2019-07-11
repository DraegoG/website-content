---
title: "The Go Empty Interface Explained"
description: "Interfaces, interface{}, conversions"
date: 2017-07-21T00:47:59+02:00
tags: go
---

An interface in Go specifies a **method set**. Any type that implements this method set is said to **implement the interface**.

An interface is implemented implicity. There is no _implements_ keyword, used in other languages. If a type defines the entire method set of an interface, it implements it. It's called structural typing, the compile-time equivalent of [duck typing](https://en.wikipedia.org/wiki/Duck_typing).

> If it walks like duck, swims like a duck and quacks like a duck, it's a duck

Important: in Go, interface abstract a set of methods (actions), not data.

## Example

The following example taken from [How to use interfaces in Go](http://jordanorelli.com/post/32665860244/how-to-use-interfaces-in-go) illustrates a basic interface of an Animal that can Speak, and different structs that satisfy the interface:

```go
type Animal interface {
    Speak() string
}

type Dog struct {
}

func (d Dog) Speak() string {
    return "Woof!"
}

type Cat struct {
}

func (c Cat) Speak() string {
    return "Meow!"
}

type Llama struct {
}

func (l Llama) Speak() string {
    return "?????"
}

type JavaProgrammer struct {
}

func (j JavaProgrammer) Speak() string {
    return "Design patterns!"
}
```

You can build an []Animal and run `Speak()` on its content:

```go
func main() {
    animals := []Animal{Dog{}, Cat{}, Llama{}, JavaProgrammer{}}
    for _, animal := range animals {
        fmt.Println(animal.Speak())
    }
}
```

[play](https://play.golang.org/p/yGTd4MtgD5)

## The empty interface

The `Animal` interface is small and nice, but there's something even simpler, yet somewhat a complex concept to understand for beginners: the empty interface.

`interface{}` is the Go empty interface, a key concept. Every type implements it by definition.

An interface is a type, so you can define for example:

```go
type Dog struct {
    Age interface{}
}
```

and you can also pass an empty interface type as a function parameter:

```go
func Eat(t interface{}) {
    // ...
}
```

Accepting `interface{}` doesn't mean the function accepts any type, but rather means that Eat accepts a value of `interface{}` type.

At runtime, Go will convert the actual value passed to an `interface{}` value.

If you define a field in a struct with type `interface{}`, you can assign it a value of any type. For example:

```go
package main

import "fmt"

type Dog struct {
    Age interface{}
}

func main() {
    dog := Dog{}
    dog.Age = "3"
    fmt.Printf("%#v %T\n", dog.Age, dog.Age)

    dog.Age = 3
    fmt.Printf("%#v %T\n", dog.Age, dog.Age)

    dog.Age = "not really an age"
    fmt.Printf("%#v %T", dog.Age, dog.Age)
}
```

[play](https://play.golang.org/p/D57Zdnf9Ik)

prints

```sh
"3" string
3 int
"not really an age" string
```

Of course this is not limited to basic types: you could store a slice, a map, any custom struct in there.

## How interface are represented internally

Internally, an interface _value_ is two [`words`](https://en.wikipedia.org/wiki/Word_(computer_architecture)), sets of bytes.

One word points to the value underlying type.
One word points to the data.

## Conversions

When we did `animals := []Animal{Dog{}, Cat{}, Llama{}, JavaProgrammer{}}` previously, Go automatically converted all our specific animal types to an Animal type. Every element of that slice is now type Animal, with the underlying type pointing to the specific species, like Dog, Cat and Llama.

But if a method accepts `[]interface{}` for example, we cannot just pass `animals` to it, because the type does not match. We need to **explicitly convert each `Animal` to an `interface{}`** before, with a loop, like described in the [Can I convert a []T to an []interface{}](https://golang.org/doc/faq#convert_slice_of_interface) FAQ:

```go
t := []int{1, 2, 3, 4}
s := make([]interface{}, len(t))
for i, v := range t {
    s[i] = v
}
```

## Determine the underlying type of an `interface{}`

If a value is of type `interface{}`, you might want to determine the underlying type. How? With a switch on `.(type)`, like [Effective Go](https://golang.org/doc/effective_go.html#type_switch) explains:

> A switch can also be used to discover the dynamic type of an interface variable. Such a type switch uses the syntax of a type assertion with the keyword type inside the parentheses. If the switch declares a variable in the expression, the variable will have the corresponding type in each clause. It's also idiomatic to reuse the name in such cases, in effect declaring a new variable with the same name but a different type in each case.

```go
var t interface{}
t = functionOfSomeType()
switch t := t.(type) {
default:
    fmt.Printf("unexpected type %T\n", t)     // %T prints whatever type t has
case bool:
    fmt.Printf("boolean %t\n", t)             // t has type bool
case int:
    fmt.Printf("integer %d\n", t)             // t has type int
case *bool:
    fmt.Printf("pointer to boolean %t\n", *t) // t has type *bool
case *int:
    fmt.Printf("pointer to integer %d\n", *t) // t has type *int
}
```
