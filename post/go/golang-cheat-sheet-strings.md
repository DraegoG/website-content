---
title: "Go Strings Cheat Sheet"
date: 2017-07-16T13:53:51+02:00
tags: go
---

<!-- TOC -->

- [Check if a string starts with a substring](#check-if-a-string-starts-with-a-substring)
- [Check if a string ends with a substring](#check-if-a-string-ends-with-a-substring)
- [Calculate the maximum string length in a slice of strings](#calculate-the-maximum-string-length-in-a-slice-of-strings)
- [Comparing strings case insensitive](#comparing-strings-case-insensitive)

<!-- /TOC -->

## Check if a string starts with a substring

```go
package main

import (
    "strings"
)

func main() {
    strings.HasPrefix("flavio", "fla") // true
}
```
[play](https://play.golang.org/p/lv_mIHoQOf)

## Check if a string ends with a substring

```go
package main

import (
    "strings"
)

func main() {
    strings.HasSuffix("flavio", "vio") // true
}
```
[play](https://play.golang.org/p/FDwPGkQ2Sa)

## Calculate the maximum string length in a slice of strings

```go
// calculatemaxwidth given a slice of strings calculates the maximum
// length
func calculatemaxwidth(lines []string) int {
    w := 0
    for _, l := range lines {
        len := utf8.RuneCountInString(l)
        if len > w {
            w = len
        }
    }

    return w
}
```

## Comparing strings case insensitive

Instead of running `ToUpper()` or `ToLower()` from the `strings` or `bytes` packages, use [`strings.EqualFold()`](https://golang.org/pkg/strings/#EqualFold) or [`bytes.EqualFold()`](https://golang.org/pkg/bytes/#EqualFold), because they are guaranteed to work across all languages.

```go
package main

import (
	"bytes"
	"fmt"
)

func main() {
	fmt.Println(bytes.EqualFold([]byte("Go"), []byte("go")))
}
```