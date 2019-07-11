---
title: "Go Data Structures: Hash Table"
date: 2017-08-09T16:04:59+02:00
description: Analysis and implementation of the Hash Table data structure in Go
tags: go
---

An Hash Table is a hash implementation of a hash table data structure. Instead of using a custom key to store the value in a map, the data structure performs a hashing function on the key to return the exact index of an item in the array.

## Implementation

Internally the hash table will be represented with a `map` type, and I'll expose the

- `Put()`
- `Remove()`
- `Get()`
- `Size()`

methods.

I'll create a `ValueHashtable` generic type, concurrency safe, that can generate hash tables containing any type. Keys can be any type as long as it implements the `Stringer` interface. By running `go generate` the code will create a type-specific Hash Table implementation, encapsulating the actual value-specific data structure containing the data.

```go
// Package hashtable creates a ValueHashtable data structure for the Item type
package hashtable

import (
    "fmt"
    "sync"

    "github.com/cheekybits/genny/generic"
)

// Key the key of the dictionary
type Key generic.Type

// Value the content of the dictionary
type Value generic.Type

// ValueHashtable the set of Items
type ValueHashtable struct {
    items map[int]Value
    lock  sync.RWMutex
}

// the hash() private function uses the famous Horner's method
// to generate a hash of a string with O(n) complexity
func hash(k Key) int {
    key := fmt.Sprintf("%s", k)
    h := 0
    for i := 0; i < len(key); i++ {
        h = 31*h + int(key[i])
    }
    return h
}

// Put item with value v and key k into the hashtable
func (ht *ValueHashtable) Put(k Key, v Value) {
    ht.lock.Lock()
    defer ht.lock.Unlock()
    i := hash(k)
    if ht.items == nil {
        ht.items = make(map[int]Value)
    }
    ht.items[i] = v
}

// Remove item with key k from hashtable
func (ht *ValueHashtable) Remove(k Key) {
    ht.lock.Lock()
    defer ht.lock.Unlock()
    i := hash(k)
    delete(ht.items, i)
}

// Get item with key k from the hashtable
func (ht *ValueHashtable) Get(k Key) Value {
    ht.lock.RLock()
    defer ht.lock.RUnlock()
    i := hash(k)
    return ht.items[i]
}

// Size returns the number of the hashtable elements
func (ht *ValueHashtable) Size() int {
    ht.lock.RLock()
    defer ht.lock.RUnlock()
    return len(ht.items)
}
```

## Tests

The tests describe the usage of the above implementation. Notice that we never interact with the underlying `map` type, which might as well be implemented in another way if only Go didn't provide us a map type already.

```go
package hashtable

import (
    "fmt"
    "testing"
)

func populateHashtable(count int, start int) *ValueHashtable {
    dict := ValueHashtable{}
    for i := start; i < (start + count); i++ {
        dict.Put(fmt.Sprintf("key%d", i), fmt.Sprintf("value%d", i))
    }
    return &dict
}

func TestPut(t *testing.T) {
    dict := populateHashtable(3, 0)
    if size := dict.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
    dict.Put("key1", "value1") //should not add a new one, just change the existing one
    if size := dict.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
    dict.Put("key4", "value4") //should add it
    if size := dict.Size(); size != 4 {
        t.Errorf("wrong count, expected 4 and got %d", size)
    }
}

func TestRemove(t *testing.T) {
    dict := populateHashtable(3, 0)
    dict.Remove("key2")
    if size := dict.Size(); size != 2 {
        t.Errorf("wrong count, expected 2 and got %d", size)
    }
}
```

## Creating a concrete hash table data structure

You can use this generic implemenation to generate type-specific hash tables, using

```bash
//generate a `IntHashtable` hash table of `int` values
genny -in hashtable.go -out hashtable-int.go gen "Value=int"

//generate a `StringHashtable` hash table of `string` values
genny -in hashtable.go -out hashtable-string.go gen "Value=string"
```

