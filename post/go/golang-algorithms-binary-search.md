---
title: "Binary Search Algorithm Implemented in Go"
seotitle: "Golang Binary Search Algorithm"
description: How to implement the Binary Search Algorithm in Go
date: 2017-07-24T09:07:09+02:00
tags: go
---

**Binary Search** is a simple algorithm to find an item in an _sorted array_, and it's usually referenced as a code sample to study when learning a new programming language.

## Efficency

It's very efficient:

- Time: **O(log n)**, it's at worst logaritmic
- Space: **0(1)**, takes constant time

## Theory

Given a sorted array, we pick the item Y in the middle and we compare it to the target value X.

If Y matches X, we return the Y position and we exit.

We determine if X < Y, in this case we discard the right side, and we go in the middle of the left side, and we repeat the same operation as above.

The search ends when Y finally matches X. If this does not happen, we return the position that X would have taken if it was in the array.

## Implementation

We're lucky, the Go standard library provides a binary tree implementation in its `sort` package, in [`sort.Search()`](https://golang.org/pkg/sort/#Search).

Let's see the usage of the API, as taken from the package documentation, so we know what `sort.Search` should return:

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    a := []int{1, 3, 6, 10, 15, 21, 28, 36, 45, 55}
    x := 6

    i := sort.Search(len(a), func(i int) bool { return a[i] >= x })
    if i < len(a) && a[i] == x {
        fmt.Printf("found %d at index %d in %v\n", x, i, a)
    } else {
        fmt.Printf("%d not found in %v\n", x, a)
    }
}
```

`sort.Search` returns an index `i`, and we just need to make sure that that index actually contains `x`.

Of course we want to know how this is implemented internally. Since the standard library is written in Go, and open source, it's really easy to see how `sort.Search` is implemented:

```go
func Search(n int, f func(int) bool) int {
    // Define f(-1) == false and f(n) == true.
    // Invariant: f(i-1) == false, f(j) == true.
    i, j := 0, n
    for i < j {
        h := i + (j-i)/2 // avoid overflow when computing h
        // i ≤ h < j
        if !f(h) {
            i = h + 1 // preserves f(i-1) == false
        } else {
            j = h // preserves f(j) == true
        }
    }
    // i == j, f(i-1) == false, and f(j) (= f(i)) == true  =>  answer is i.
    return i
}
```

Let's break it down:

Given an array with length `n`, and a comparison function `f` (that internally evaluates `x >= a[h]`), we start iterating the array `a`.

Let's use the actual values we use in the example, it's easier to show what's happening.

Data:

```go
a := []int{1, 3, 6, 10, 15, 21, 28, 36, 45, 55}
x := 6
```

Iteration 1:

- `i` is `0`, `j` is `9`.
- `h` is calculated as `(0 + (9-0) / 2)` = `4`
- `a[h]` is `15`. This means we execute `j = h`

Iteration 2:

- `i` is `0`, `j` is `4`.
- `h` is calculated as `(0 + (4-0) / 2)` = `2`
- `a[h]` is `6`. We found the position of `x`, this means we return `h = 2`

## Searching reverse order

Since we can pass a function to `sort.Search`, it's easy to search on an array sorted in the reverse order, like

```go
a := []int{55, 45, 36, 28, 21, 15, 10, 6, 3, 1}
x := 6
```

by passing a function that compares `a[i] <= x` instead of `a[i] >= x`.

```go
i := sort.Search(len(a), func(i int) bool { return a[i] <= x })
```
