---
title: "Sorting a map type in Go"
date: 2016-08-16T14:49:08+02:00
tags: go
---

One of the peculiarities of a Go map is that the fields return in a random order.

If you run this simple example:

```go
package main

import (
	"fmt"
)

func main() {
	ages := map[string]int{
		"a": 1,
		"c": 3,
		"d": 4,
		"b": 2,
	}

	fmt.Println(ages)
	fmt.Println(ages)
	fmt.Println(ages)
}
```
[play](https://play.golang.org/p/RUKIhyRb_x)

the output will be

```sh
map[b:2 a:1 c:3 d:4]
map[c:3 d:4 b:2 a:1]
map[d:4 b:2 a:1 c:3]
```

This is on purpose, to avoid relying on the items order, as different implementations of the compiler might use different hash functions. It's one of those things that make Go very explicit in avoiding causing invalid assumptions.

What if you want to order a map by key?

```go
package main

import (
	"fmt"
	"sort"
)

func main() {
	ages := map[string]int{
		"a": 1,
		"c": 3,
		"d": 4,
		"b": 2,
	}

	names := make([]string, 0, len(ages))

	for name := range ages {
		names = append(names, name)
	}

	sort.Strings(names) //sort keys alphabetically

	for _, name := range names {
		fmt.Println(ages[name])
	}

}
```
[play](https://play.golang.org/p/k_18NDecya)

This program will print the values of the map, ordered by key:

```sh
1
2
3
4
```

