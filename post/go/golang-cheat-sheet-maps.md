---
title: "Go Maps Cheat Sheet"
date: 2017-08-07T13:53:51+02:00
tags: go
---

<!-- TOC -->

- [Create map](#create-map)
- [Add item to map](#add-item-to-map)
- [Lookup item from map](#lookup-item-from-map)
- [Delete item from map](#delete-item-from-map)
- [Delete all content from a map](#delete-all-content-from-a-map)
- [Count the items in a map](#count-the-items-in-a-map)
- [Put the keys of a map into a slice](#put-the-keys-of-a-map-into-a-slice)

<!-- /TOC -->

## Create map

```go
// define map
var m1 map[int]string

// instantiate map
m1 = make(map[int]string)

// implict map instantiation
m2 := make(map[int]string)

// map literal
m3 := map[int]string{
    1:  "One",
    9:  "Nine"
}
```

## Add item to map

```go
m := map[int]string{
    1:  "One",
    9:  "Nine"
}
m[10] = "Ten"

// m contains 1, 9, 10
```

## Lookup item from map

```go
m := map[int]string{
    1:  "One",
    9:  "Nine"
}
item, ok := m[9]   //item is "Nine; ok is true if the
                    //key was found, false otherwise
```

## Delete item from map

```go
m := map[int]string{
    1:  "One",
    9:  "Nine"
}
delete(m, 9)
//m contains only the `1` item
```

## Delete all content from a map

Assign to the variable pointing to the map a new map:

```go
m := map[int]string{
    1:  "One",
    9:  "Nine"
}
m = make(map[int]string) // m is an initialized, empty map
```

## Count the items in a map

```go
m := map[int]string{
    1:  "One",
    9:  "Nine"
}
l := len(m) // l == 2
```

## Put the keys of a map into a slice

```go
keys := make([]string, 0, len(m))
for k := range m {
    keys = append(keys, k)
}
```