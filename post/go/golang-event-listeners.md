---
title: "Implement Events Listeners in Go through Channels"
date: 2017-08-10T11:04:59+02:00
tags: go
---

This post aims to explain how to implement an event listener using Go channels, what one could call an observer in design pattern terms.

## The problem

I have a dog that sometimes barks, and when this happens I usually tell him not to bark. And as all dogs, he sometimes poops so I need to pick it up.

I'll model my dog as a struct that has a list of event listeners, that is a list of people that take care of him.

The dog will emit events to those listeners when something happens.

Here's how we'd model our dog in Go: we have a struct with a name and a list of caretakers, and 3 events: we can add a new dog sitter, we can remove one, and our dog can emit events.

```go
// Dog has a name and a list of people caring for him and watching
// what he does
type Dog struct {
    name    string
    sitters map[string][]chan string
}

// AddSitter adds an event listener to the Dog struct instance
func (b *Dog) AddSitter(e string, ch chan string) {
    if b.sitters == nil {
        b.sitters = make(map[string][]chan string)
    }
    if _, ok := b.sitters[e]; ok {
        b.sitters[e] = append(b.sitters[e], ch)
    } else {
        b.sitters[e] = []chan string{ch}
    }
}

// RemoveSitter removes an event listener from the Dog struct instance
func (b *Dog) RemoveSitter(e string, ch chan string) {
    if _, ok := b.sitters[e]; ok {
        for i := range b.sitters[e] {
            if b.sitters[e][i] == ch {
                b.sitters[e] = append(b.sitters[e][:i], b.sitters[e][i+1:]...)
                break
            }
        }
    }
}

// Emit emits an event on the Dog struct instance
func (b *Dog) Emit(e string, response string) {
    if _, ok := b.sitters[e]; ok {
        for _, handler := range b.sitters[e] {
            go func(handler chan string) {
                handler <- response
            }(handler)
        }
    }
}
```
## Running our dog around

Let's take the dog into the world and see how it works. First I'm the only one taking care of the dog, so I'll add myself as the dog sitter with `balto.AddSitter()` for all the events I can handle: `bark`, `poop`, `hungry`.

After a while I got tired of picking up the poop and I hired a dogsitter to go around and do the job for me, but I'll still handle telling the dog not to bark, and feed him.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    balto := Dog{"Balto", nil}

    flavio := make(chan string)

    balto.AddSitter("bark", flavio)
    balto.AddSitter("poop", flavio)
    balto.AddSitter("hungry", flavio)

    go func() {
        for {
            msg := <-flavio
            fmt.Println("Flavio: " + msg)
        }
    }()

    fmt.Println("The dog barked!")
    balto.Emit("bark", "Told not to bark!")

    fmt.Println("The dog pooped!")
    balto.Emit("poop", "Picked up poop!")

    fmt.Println("The dog is hungry!")
    balto.Emit("hungry", "Feed the dog!")

    time.Sleep(3 * time.Second)

    fmt.Printf("\n.\n.\n.\n")
    balto.RemoveSitter("poop", flavio)

    // Hired a dog sitter to pick up poop
    dogsitter := make(chan string)
    balto.AddSitter("poop", dogsitter)
    fmt.Println("Flavio hired a dogsitter to pick up poop, won't pick it up again")

    go func() {
        for {
            msg := <-dogsitter
            fmt.Println("Dogsitter: " + msg)
        }
    }()

    fmt.Println("Dog barked!")
    balto.Emit("bark", "Told not to bark!")

    fmt.Println("Dog has pooped!")
    balto.Emit("poop", "Picked up poop!")
    fmt.Println("Dog has pooped again!")
    balto.Emit("poop", "Picked up poop, again!")
    fmt.Println("The dog is hungry!")
    balto.Emit("hungry", "Feed the dog!")

    fmt.Scanln()
}
```

I'm using `fmt.Scanln()` at the end to prevent the program to exit when `main()` is over, while still waiting for the goroutines handling events to complete.

If I run it, it seems our new hire is doing the work we expect him too, and we can relax:

```bash
$ go run eventlistener.go
The dog barked!
The dog pooped!
The dog is hungry!
Flavio: Picked up poop!
Flavio: Told not to bark!
Flavio: Feed the dog!

.
.
.
Flavio hired a dogsitter to pick up poop, won't pick it up again
Dog barked!
Dog has pooped!
Dog has pooped again!
The dog is hungry!
Flavio: Told not to bark!
Dogsitter: Picked up poop!
Dogsitter: Picked up poop, again!
Flavio: Feed the dog!
```