---
title: "Making a copy of a struct in Go"
date: 2016-04-05T11:04:59+02:00
tags: go
---

A struct variable in Go can be copied to another variable very easily using the assignment statement:

```go
package main

import (
	"fmt"
)

type Dog struct {
	age  int
	name string
}

func main() {
	roger := Dog{5, "Roger"}
	mydog := roger
	if roger == mydog {
		fmt.Println("Roger and mydog are equal structs")
	}
}
```
[play](https://play.golang.org/p/vArVyugMym)

`mydog` and `roger` are two separate variables, but comparing them property-by-property they are exactly the same.

We can now modify every property of those variables without affecting the other object, because the `Dog` struct contains basic types, which are copied by value.

If we had a reference type in our struct, this was not that easy, because the `pointer` would be copied, not the value, so it would have been a _shallow copy_.

For example

```go
type Cat struct {
    age int
    name string
    friends []string
}
```

The list of friends of our cat is a slice, a reference type (along with pointers, maps, functions and channels), so if you had a cat object and you copy it like we did for the Dog example above, you couldn't modify the friends property without affecting the other object as well.

A **deep copy** is needed.

## Deep copy a struct

You can perform such deep copy manually. In the case of a slice, you can perform the copy like this:

```go
package main

import (
	"fmt"
)

type Cat struct {
	age     int
	name    string
	friends []string
}

func main() {
	wilson := Cat{7, "Wilson", []string{"Tom", "Tabata", "Willie"}}
	nikita := wilson

	nikita.friends = make([]string, len(wilson.friends))
	copy(nikita.friends, wilson.friends)

	nikita.friends = append(nikita.friends, "Syd")

	fmt.Println(wilson)
	fmt.Println(nikita)
}
```
[play](https://play.golang.org/p/HW_UUDPbTm)

The above code will result in **wilson** being `{7 Wilson [Tom Tabata Willie]}`
and **nikita** being `{7 Wilson [Tom Tabata Willie Syd]}`

So you can see the slice is a completely different object, not just a reference to the same slice.

## Using a deep copy library

<https://github.com/jinzhu/copier> is (one of the many) deep copy libs/helpers out there. It makes it really easy to deep copy a struct without explicitly managing each field. Here's an example, all we need is `copier.Copy(&nikita, &wilson)` and we're set:

```go
package main

import (
	"fmt"
	"github.com/jinzhu/copier"
)

type Cat struct {
	age     int
	name    string
	friends []string
}

func main() {
	wilson := Cat{7, "Wilson", []string{"Tom", "Tabata", "Willie"}}
	nikita := Cat{}
	copier.Copy(&nikita, &wilson)

	nikita.friends = append(nikita.friends, "Syd")

	fmt.Println(wilson)
	fmt.Println(nikita)
}
```
