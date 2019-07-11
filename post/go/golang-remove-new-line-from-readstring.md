---
title: "Go, remove the io.Reader.ReadString newline char"
description: "Go: remove the new line char from a string acquired using io.Reader.ReadString"
date: 2017-08-23T16:04:59+02:00
updated: 2018-05-28T16:04:59+02:00
tags: go
---

Suppose you I want to get a number from stdin, using `io.Reader.ReadString`, and you want to convert this number to an integer.

Before being able to convert it to integer using `strconv.Atoi`, you have to remove the new line char.

How can you do so?

## Solution

Using `strings.TrimSuffix`:

```go
package main

import (
	"bufio"
	"os"
	"strings"
)

func main() {
	reader := bufio.NewReader(os.Stdin)
	text, _ := reader.ReadString('\n')
	text = strings.TrimSuffix(text, "\n")
}
```