---
title: "Go Data Structures: Stack"
date: 2017-08-10T18:04:59+02:00
description: Analysis and implementation of the Stack data structure in Go
tags: go
---

A stack is an ordered collection of items following the Last-In-First-Out (LIFO) principle. We add and remove items from the same part of the pile, called the top. We cannot remove items from the base. Just like a pile of books.

Stacks have tons of uses, from creating a history of pages visited to commands entered and to store actions that can be undone.

## Implementation

Internally the stack will be represented with a `slice` type, and I'll expose the

- `Push()`
- `Pull()`
- `New()`

methods.

`New()` serves as the constructor, which initializes the internal slice when we start using it.

I'll create an `ItemStack` generic type, concurrency safe, that can generate stacks containing any type by using `genny`, to create a type-specific stack implementation, encapsulating the actual value-specific data structure containing the data.

```go
// Package stack creates a ItemStack data structure for the Item type
package stack

import (
    "sync"

    "github.com/cheekybits/genny/generic"
)

// Item the type of the stack
type Item generic.Type

// ItemStack the stack of Items
type ItemStack struct {
    items []Item
    lock  sync.RWMutex
}

// New creates a new ItemStack
func (s *ItemStack) New() *ItemStack {
    s.items = []Item{}
    return s
}

// Push adds an Item to the top of the stack
func (s *ItemStack) Push(t Item) {
    s.lock.Lock()
    s.items = append(s.items, t)
    s.lock.Unlock()
}

// Pop removes an Item from the top of the stack
func (s *ItemStack) Pop() *Item {
    s.lock.Lock()
    item := s.items[len(s.items)-1]
    s.items = s.items[0 : len(s.items)-1]
    s.lock.Unlock()
    return &item
}
```

## Tests

The tests describe the usage of the above implementation.

```go
package stack

import (
    "testing"
)

var s ItemStack

func initStack() *ItemStack {
    if s.items == nil {
        s = ItemStack{}
        s.New()
    }
    return &s
}

func TestPush(t *testing.T) {
    s := initStack()
    s.Push(1)
    s.Push(2)
    s.Push(3)
    if size := len(s.items); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
}

func TestPop(t *testing.T) {
    s.Pop()
    if size := len(s.items); size != 2 {
        t.Errorf("wrong count, expected 2 and got %d", size)
    }

    s.Pop()
    s.Pop()
    if size := len(s.items); size != 0 {
        t.Errorf("wrong count, expected 0 and got %d", size)
    }
}
```

## Creating a concrete stack data structure

You can use this generic implemenation to generate type-specific stacks, using

```bash
//generate a `IntStack` stack of `int` values
genny -in stack.go -out stack-int.go gen "Item=int"

//generate a `StringStack` stack of `string` values
genny -in stack.go -out stack-string.go gen "Item=string"
```

