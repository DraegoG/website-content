---
title: "Go, append a slice of strings to a file"
date: 2017-07-31T19:53:51+02:00
tags: go
---

The following snippet shows how to print the content of a slice of strings into a file, separating each string with a new line.

```go
package main

func main() {
    var text []string

    //... fill text with string values

    // writes a slice of strings to a file, one per line
    sep := "\n"
    for _, line := range text {
        if _, err = f.WriteString(line + sep); err != nil {
            panic(err)
        }
    }
}
```