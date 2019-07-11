---
title: "Is Go object oriented?"
date: 2017-08-13T15:46:52+02:00
tags: go
---

Sometimes I read an article that says "Go is object oriented". Sometimes another article that claims that no object oriented programming can be done with Go, just because it does not have classes.

So I wrote this post to clarify this topic. Is Go object oriented, or not?

If you're used to think in a particular language, depending on which language you're coming from, you might have a different take on this topic. For example if you come from C, clearly Go has lots more object oriented programming features. Coming from Java, Go code doesn't look much object oriented.

What you need to do in this case is stop thinking in terms of the "other language", and think with a Go mindset first.

Here's my answer: **Yes**, Go is object oriented, and in a **refreshing** a **sane** way.

The [Go FAQ](https://golang.org/doc/faq#Is_Go_an_object-oriented_language) says:

> ### Is Go an object-oriented language?

> Yes and no. Although Go has types and methods and allows an object-oriented style of programming, there is no type hierarchy. The concept of “interface” in Go provides a different approach that we believe is easy to use and in some ways more general. There are also ways to embed types in other types to provide something analogous—but not identical—to subclassing. Moreover, methods in Go are more general than in C++ or Java: they can be defined for any sort of data, even built-in types such as plain, “unboxed” integers. They are not restricted to structs (classes).

> Also, the lack of a type hierarchy makes “objects” in Go feel much more lightweight than in languages such as C++ or Java.

## Cherry-picking concepts

Go picked some concepts from procedural programming, functional programming and object oriented programming, and put them together, and left out other concepts to create its own unique flavour of idiomatic programming style.

## No classes, enter structs

There are no classes in Go, in their traditional concept, but Go has struct types, which are much more powerful than their C counterpart. Struct types plus their associated methods serve the same goal of a traditional class, where the struct only holds the state, not the behavior, and the methods provide them behavior, by allowing to change the state.

## Encapsulation

One of the best features of Go: capitalized fields, methods and functions are public. All the other fields are local to the package and not exported. With a single look you know if something is public or private. There's no _protected_ because there is no inheritance.

## No inheritance

There is no concept of inheritance. From the Go FAQ:

> Object-oriented programming, at least in the best-known languages, involves too much discussion of the relationships between types, relationships that often could be derived automatically. Go takes a different approach.

## Composition over inheritance

This [well known principle](https://en.wikipedia.org/wiki/Composition_over_inheritance), also mentioned in the Gang of Four book, is found a lot in Go code.

When declaring a struct we can add an unnamed (anonymous) field, which causes its fields and its methods to be exposed on the struct. This is called **struct embedding**:

```go
package main

import (
	"fmt"
)

type Dog struct {
	Animal
}
type Animal struct {
	Age int
}

func (a *Animal) Move() {
	fmt.Println("Animal moved")
}
func (a *Animal) SayAge() {
	fmt.Printf("Animal age: %d\n", a.Age)
}
func main() {
	d := Dog{}
	d.Age = 3
	d.Move()
	d.SayAge()
}
```
[play](https://play.golang.org/p/IxMoeByWp5)

## Interfaces

Forget Java and PHP-style interfaces. Go interfaces are very different, and one key concept is that interfaces are satisfied **implicitly**.

From the Go FAQ:

> Rather than requiring the programmer to declare ahead of time that two types are related, in Go a type automatically satisfies any interface that specifies a subset of its methods.

Interfaces are typically very small, up to being just one method. You won't see long lists of methods in idiomatic Go.

Interfaces elegantly provide **polymorphism**: by accepting an interface, you declare to accept any kind of object satisfying that interface.

## Methods

Types have methods. They are defined outside the type definition, with a syntax that might recall the [JavaScript](/javascript/) prototype method definitions:

```js
function Person(first, last) {
    this.firstName = first;
    this.lastName = last;
}
Person.prototype.name = function() {
    return this.firstName + " " + this.lastName;
};
p = new Person("Flavio", "Copes")
p.name() // Flavio Copes
```

in Go the same code is written as:

```go
package main

import (
	"fmt"
)
type Person struct {
	firstName string
	lastName  string
}
func (p Person) name() string {
	return p.firstName + " " + p.lastName
}
func main() {
	p := Person{"Flavio", "Copes"}
	fmt.Println(p.name())
}
```

## Attach methods to types

Methods can be attached to any type, even basic data types. Since methods can only be attached in the same package where the type is defined, we cannot "enrich" the built-in basic types, but we can enrich any named type we create with a base type underlying representation:

```go
package main

import (
	"fmt"
)

type Amount int

func (a *Amount) Add(add Amount) {
	*a += add
}

func main() {
	var a Amount
	a = 1
	a.Add(2)
	fmt.Println(a)
}
```
[play](https://play.golang.org/p/ONlUmue1jA)

## Functions

Think about a traditional object oriented programming language like Java. How many times did you define a "Utils" class with static methods?

This is to workaround the notion that everything is an object, and function definitions must be inside classes. Such thing does not happen with Go, because Go has functions. Not everything needs to be an object, or a method, in the real world. "Classes" and "objects" are very useful but they cannot be used for everything.

In Go not everything is an object (and technically nothing is an object, but some people call type values and variables "objects"), methods are functions associated to a type, but Go also allows functions to live outside an object, just like C functions.

So, although Go allows methods, it also allows functions, and **first class functions** (functions can be stored as struct fields, can be passed as arguments to other functions, can be returned from a function or methods return value).

## Less bloat

Overall the Go implementation of object oriented programming is incredibly **flexible** and **direct**. Leaving behind classes and inheritance, you'll see very little boilerplate, and instead of reasoning about the perfect hierarchical structure for classes, which becomes hard to change, you have the freedom to compose and decompose types as needed.
