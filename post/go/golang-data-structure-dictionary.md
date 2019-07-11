---
title: "Go Data Structures: Dictionary"
date: 2017-08-09T11:04:59+02:00
description: Analysis and implementation of the Dictionary data structure in Go
tags: go
---

A dictionary stores `[key, value]` pairs. Go provides a very convenient implementation of a dictionary by its built-in `map` type.

In this article I'll enrich the `map` built-in type with some convenient operations to get information out of it, and to change its content.

I'll create a `ItemDictionary` generic type, concurrency safe, that can generate dictionaries for any type. By running `genny` the code will create a type-specific Dictionary implementation, encapsulating the actual `map` containing the data.

##  Goal

The dictionary is created using `dict := ValueDictionary{}` and provides this set of exported methods:

- `Set()`
- `Delete()`
- `Has()`
- `Get()`
- `Clear()`
- `Size()`
- `Keys()`
- `Values()`

## Implementation

```go
// Package dictionary creates a ValueDictionary data structure for the Item type
package dictionary

import (
    "sync"

    "github.com/cheekybits/genny/generic"
)

// Key the key of the dictionary
type Key generic.Type

// Value the content of the dictionary
type Value generic.Type

// ValueDictionary the set of Items
type ValueDictionary struct {
    items map[Key]Value
    lock  sync.RWMutex
}

// Set adds a new item to the dictionary
func (d *ValueDictionary) Set(k Key, v Value) {
    d.lock.Lock()
    defer d.lock.Unlock()
    if d.items == nil {
        d.items = make(map[Key]Value)
    }
    d.items[k] = v
}

// Delete removes a value from the dictionary, given its key
func (d *ValueDictionary) Delete(k Key) bool {
    d.lock.Lock()
    defer d.lock.Unlock()
    _, ok := d.items[k]
    if ok {
        delete(d.items, k)
    }
    return ok
}

// Has returns true if the key exists in the dictionary
func (d *ValueDictionary) Has(k Key) bool {
    d.lock.RLock()
    defer d.lock.RUnlock()
    _, ok := d.items[k]
    return ok
}

// Get returns the value associated with the key
func (d *ValueDictionary) Get(k Key) Value {
    d.lock.RLock()
    defer d.lock.RUnlock()
    return d.items[k]
}

// Clear removes all the items from the dictionary
func (d *ValueDictionary) Clear() {
    d.lock.Lock()
    defer d.lock.Unlock()
    d.items = make(map[Key]Value)
}

// Size returns the amount of elements in the dictionary
func (d *ValueDictionary) Size() int {
    d.lock.RLock()
    defer d.lock.RUnlock()
    return len(d.items)
}

// Keys returns a slice of all the keys present
func (d *ValueDictionary) Keys() []Key {
    d.lock.RLock()
    defer d.lock.RUnlock()
    keys := []Key{}
    for i := range d.items {
        keys = append(keys, i)
    }
    return keys
}

// Values returns a slice of all the values present
func (d *ValueDictionary) Values() []Value {
    d.lock.RLock()
    defer d.lock.RUnlock()
    values := []Value{}
    for i := range d.items {
        values = append(values, d.items[i])
    }
    return values
}
```

## Tests

The tests describe the usage of the above implementation. Notice that we never interact with the underlying `map` type, which might as well be implemented in another way if only Go didn't provide us a map type already.

```go
package dictionary

import (
    "fmt"
    "testing"
)

func populateDictionary(count int, start int) *ValueDictionary {
    dict := ValueDictionary{}
    for i := start; i < (start + count); i++ {
        dict.Set(fmt.Sprintf("key%d", i), fmt.Sprintf("value%d", i))
    }
    return &dict
}

func TestSet(t *testing.T) {
    dict := populateDictionary(3, 0)
    if size := dict.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
    dict.Set("key1", "value1") //should not add a new one, just change the existing one
    if size := dict.Size(); size != 3 {
        t.Errorf("wrong count, expected 3 and got %d", size)
    }
    dict.Set("key4", "value4") //should add it
    if size := dict.Size(); size != 4 {
        t.Errorf("wrong count, expected 4 and got %d", size)
    }
}

func TestDelete(t *testing.T) {
    dict := populateDictionary(3, 0)
    dict.Delete("key2")
    if size := dict.Size(); size != 2 {
        t.Errorf("wrong count, expected 2 and got %d", size)
    }
}

func TestClear(t *testing.T) {
    dict := populateDictionary(3, 0)
    dict.Clear()
    if size := dict.Size(); size != 0 {
        t.Errorf("wrong count, expected 0 and got %d", size)
    }
}

func TestHas(t *testing.T) {
    dict := populateDictionary(3, 0)
    has := dict.Has("key2")
    if !has {
        t.Errorf("expected key2 to be there")
    }
    dict.Delete("key2")
    has = dict.Has("key2")
    if has {
        t.Errorf("expected key2 to be removed")
    }
    dict.Delete("key1")
    has = dict.Has("key1")
    if has {
        t.Errorf("expected key1 to be removed")
    }
}

func TestKeys(t *testing.T) {
    dict := populateDictionary(3, 0)
    items := dict.Keys()
    if len(items) != 3 {
        t.Errorf("wrong count, expected 3 and got %d", len(items))
    }
    dict = populateDictionary(520, 0)
    items = dict.Keys()
    if len(items) != 520 {
        t.Errorf("wrong count, expected 520 and got %d", len(items))
    }
}

func TestValues(t *testing.T) {
    dict := populateDictionary(3, 0)
    items := dict.Values()
    if len(items) != 3 {
        t.Errorf("wrong count, expected 3 and got %d", len(items))
    }
    dict = populateDictionary(520, 0)
    items = dict.Values()
    if len(items) != 520 {
        t.Errorf("wrong count, expected 520 and got %d", len(items))
    }
}

func TestSize(t *testing.T) {
    dict := populateDictionary(3, 0)
    items := dict.Values()
    if len(items) != dict.Size() {
        t.Errorf("wrong count, expected %d and got %d", dict.Size(), len(items))
    }
    dict = populateDictionary(0, 0)
    items = dict.Values()
    if len(items) != dict.Size() {
        t.Errorf("wrong count, expected %d and got %d", dict.Size(), len(items))
    }
    dict = populateDictionary(10000, 0)
    items = dict.Values()
    if len(items) != dict.Size() {
        t.Errorf("wrong count, expected %d and got %d", dict.Size(), len(items))
    }
}
```

## Creating a concrete dictionary data structure

You can use this generic implemenation to generate type-specific dictionaries, using

```bash
//generate a `IntDictionary` dictionary of `string` keys associated to `int` values
genny -in dictionary.go -out dictionary-string-int.go gen "Key=string Value=int"

//generate a `StringDictionary` dictionary of `string` keys associated to `string` values
genny -in dictionary.go -out dictionary-string-string.go gen "Key=string Value=string"
```

