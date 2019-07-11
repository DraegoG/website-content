---
title: "Go Data Structures: Linked List"
date: 2017-08-11T19:04:59+02:00
description: Analysis and implementation of the Linked List data structure in Go
tags: go
---

A linked list provides a data structure similar to an array, but with the big advantage that inserting an element in the middle of the list is very cheap, compared to doing so in an array, where we need to shift all elements after the current position.

While arrays keep all the elements in the same block of memory, next to each other, linked lists can contain elements scattered around memory, by storing a pointer to the next element.

A disadvantage over arrays on the other hand is that if we want to pick an element in the middle of the list, we don't know its address, so we need to start at the beginning of the list, and iterate on the list until we find it.

## Implementation

A linked list will provide these methods:

- `Append(t)` adds an Item t to the end of the linked list
- `Insert(i, t)` adds an Item t at position i
- `RemoveAt(i)` removes a node at position i
- `IndexOf()` returns the position of the Item t
- `IsEmpty()` returns true if the list is empty
- `Size()` returns the linked list size
- `String()` returns a string representation of the list
- `Head()` returns the first node, so we can iterate on it

I'll create an `ItemLinkedList` generic type, concurrency safe, that can generate linked lists containing any type by using `genny`, to create a type-specific linked list implementation, encapsulating the actual value-specific data structure containing the data.

```go
// Package linkedlist creates a ItemLinkedList data structure for the Item type
package linkedlist

import (
    "fmt"
    "sync"

    "github.com/cheekybits/genny/generic"
)

// Item the type of the linked list
type Item generic.Type

// Node a single node that composes the list
type Node struct {
    content Item
    next    *Node
}

// ItemLinkedList the linked list of Items
type ItemLinkedList struct {
    head *Node
    size int
    lock sync.RWMutex
}

// Append adds an Item to the end of the linked list
func (ll *ItemLinkedList) Append(t Item) {
    ll.lock.Lock()
    node := Node{t, nil}
    if ll.head == nil {
        ll.head = &node
    } else {
        last := ll.head
        for {
            if last.next == nil {
                break
            }
            last = last.next
        }
        last.next = &node
    }
    ll.size++
    ll.lock.Unlock()
}

// Insert adds an Item at position i
func (ll *ItemLinkedList) Insert(i int, t Item) error {
    ll.lock.Lock()
    defer ll.lock.Unlock()
    if i < 0 || i > ll.size {
        return fmt.Errorf("Index out of bounds")
    }
    addNode := Node{t, nil}
    if i == 0 {
        addNode.next = ll.head
        ll.head = &addNode
        return nil
    }
    node := ll.head
    j := 0
    for j < i-2 {
        j++
        node = node.next
    }
    addNode.next = node.next
    node.next = &addNode
    ll.size++
    return nil
}

// RemoveAt removes a node at position i
func (ll *ItemLinkedList) RemoveAt(i int) (*Item, error) {
    ll.lock.Lock()
    defer ll.lock.Unlock()
    if i < 0 || i > ll.size {
        return nil, fmt.Errorf("Index out of bounds")
    }
    node := ll.head
    j := 0
    for j < i-1 {
        j++
        node = node.next
    }
    remove := node.next
    node.next = remove.next
    ll.size--
    return &remove.content, nil
}

// IndexOf returns the position of the Item t
func (ll *ItemLinkedList) IndexOf(t Item) int {
    ll.lock.RLock()
    defer ll.lock.RUnlock()
    node := ll.head
    j := 0
    for {
        if node.content == t {
            return j
        }
        if node.next == nil {
            return -1
        }
        node = node.next
        j++
    }
}

// IsEmpty returns true if the list is empty
func (ll *ItemLinkedList) IsEmpty() bool {
    ll.lock.RLock()
    defer ll.lock.RUnlock()
    if ll.head == nil {
        return true
    }
    return false
}

// Size returns the linked list size
func (ll *ItemLinkedList) Size() int {
    ll.lock.RLock()
    defer ll.lock.RUnlock()
    size := 1
    last := ll.head
    for {
        if last == nil || last.next == nil {
            break
        }
        last = last.next
        size++
    }
    return size
}

// Insert adds an Item at position i
func (ll *ItemLinkedList) String() {
    ll.lock.RLock()
    defer ll.lock.RUnlock()
    node := ll.head
    j := 0
    for {
        if node == nil {
            break
        }
        j++
        fmt.Print(node.content)
        fmt.Print(" ")
        node = node.next
    }
    fmt.Println()
}

// Head returns a pointer to the first node of the list
func (ll *ItemLinkedList) Head() *Node {
    ll.lock.RLock()
    defer ll.lock.RUnlock()
    return ll.head
}

```

## Tests

The tests describe the usage of the above implementation.

```go
package linkedlist

import (
    "fmt"
    "testing"
)

var ll ItemLinkedList

func TestAppend(t *testing.T) {
    if !ll.IsEmpty() {
        t.Errorf("list should be empty")
    }

    ll.Append("first")
    if ll.IsEmpty() {
        t.Errorf("list should not be empty")
    }

    if size := ll.Size(); size != 1 {
        t.Errorf("wrong count, expected 1 and got %d", size)
    }

    ll.Append("second")
    ll.Append("third")

    if size := ll.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
}

func TestRemoveAt(t *testing.T) {
    _, err := ll.RemoveAt(1)
    if err != nil {
        t.Errorf("unexpected error %s", err)
    }

    if size := ll.Size(); size != 2 {
        t.Errorf("wrong count, expected 2 and got %d", size)
    }
}

func TestInsert(t *testing.T) {
    //test inserting in the middle
    err := ll.Insert(2, "second2")
    if err != nil {
        t.Errorf("unexpected error %s", err)
    }
    if size := ll.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }

    //test inserting at head position
    err = ll.Insert(0, "zero")
    if err != nil {
        t.Errorf("unexpected error %s", err)
    }
}

func TestIndexOf(t *testing.T) {
    if i := ll.IndexOf("zero"); i != 0 {
        t.Errorf("expected position 0 but got %d", i)
    }
    if i := ll.IndexOf("first"); i != 1 {
        t.Errorf("expected position 1 but got %d", i)
    }
    if i := ll.IndexOf("second2"); i != 2 {
        t.Errorf("expected position 2 but got %d", i)
    }
    if i := ll.IndexOf("third"); i != 3 {
        t.Errorf("expected position 3 but got %d", i)
    }
}

func TestHead(t *testing.T) {
    h := ll.Head()
    if "zero" != fmt.Sprint(h.content) {
        t.Errorf("Expected `zero` but got %s", fmt.Sprint(h.content))
    }
}
```

## Creating a concrete linked list data structure

You can use this generic implemenation to generate type-specific linked lists, using

```bash
//generate a `IntLinkedList` linked list of `int` values
genny -in linkedlist.go -out linkedlist-int.go gen "Item=int"

//generate a `StringLinkedList` linked list of `string` values
genny -in linkedlist.go -out linkedlist-string.go gen "Item=string"
```

