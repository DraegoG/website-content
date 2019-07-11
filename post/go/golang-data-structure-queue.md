---
title: "Go Data Structures: Queue"
date: 2017-08-10T19:04:59+02:00
description: Analysis and implementation of the Queue data structure in Go
tags: go
---

A queue is a an ordered collection of items following the First-In-First-Out (FIFO) principle. We add items from one end of the queue, and we retrieve items from the other end.

Queue applications have all sorts of uses, which can be easily inferred from real-world queues. It's not hard to imagine a queue representation of a supermarket line or the queue to get into a concert hall.

## Implementation

Internally the queue will be represented with a `slice` type, and I'll expose the

- `New()`
- `Enqueue()`
- `Dequeue()`
- `Front()`
- `IsEmpty()`
- `Size()`

methods.

`New()` serves as the constructor, which initializes the internal slice when we start using it.

I'll create an `ItemQueue` generic type, concurrency safe, that can generate queues containing any type by using `genny`, to create a type-specific queue implementation, encapsulating the actual value-specific data structure containing the data.

```go
// Package queue creates a ItemQueue data structure for the Item type
package queue

import (
    "sync"

    "github.com/cheekybits/genny/generic"
)

// Item the type of the queue
type Item generic.Type

// ItemQueue the queue of Items
type ItemQueue struct {
    items []Item
    lock  sync.RWMutex
}

// New creates a new ItemQueue
func (s *ItemQueue) New() *ItemQueue {
    s.items = []Item{}
    return s
}

// Enqueue adds an Item to the end of the queue
func (s *ItemQueue) Enqueue(t Item) {
    s.lock.Lock()
    s.items = append(s.items, t)
    s.lock.Unlock()
}

// Dequeue removes an Item from the start of the queue
func (s *ItemQueue) Dequeue() *Item {
    s.lock.Lock()
    item := s.items[0]
    s.items = s.items[1:len(s.items)]
    s.lock.Unlock()
    return &item
}

// Front returns the item next in the queue, without removing it
func (s *ItemQueue) Front() *Item {
    s.lock.RLock()
    item := s.items[0]
    s.lock.RUnlock()
    return &item
}

// IsEmpty returns true if the queue is empty
func (s *ItemQueue) IsEmpty() bool {
    return len(s.items) == 0
}

// Size returns the number of Items in the queue
func (s *ItemQueue) Size() int {
    return len(s.items)
}
```

## Tests

The tests describe the usage of the above implementation.

```go
package queue

import (
    "testing"
)

var s ItemQueue

func initQueue() *ItemQueue {
    if s.items == nil {
        s = ItemQueue{}
        s.New()
    }
    return &s
}

func TestEnqueue(t *testing.T) {
    s := initQueue()
    s.Enqueue(1)
    s.Enqueue(2)
    s.Enqueue(3)

    if size := s.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
}

func TestDequeue(t *testing.T) {
    s.Dequeue()
    if size := len(s.items); size != 2 {
        t.Errorf("wrong count, expected 2 and got %d", size)
    }

    s.Dequeue()
    s.Dequeue()
    if size := len(s.items); size != 0 {
        t.Errorf("wrong count, expected 0 and got %d", size)
    }

    if !s.IsEmpty() {
        t.Errorf("IsEmpty should return true")
    }
}
```

## Creating a concrete queue data structure

You can use this generic implemenation to generate type-specific queues, using

```bash
//generate a `IntQueue` queue of `int` values
genny -in queue.go -out queue-int.go gen "Item=int"

//generate a `StringQueue` queue of `string` values
genny -in queue.go -out queue-string.go gen "Item=string"
```

