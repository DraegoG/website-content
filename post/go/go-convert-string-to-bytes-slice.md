---
title: "Go, convert a string to a bytes slice"
date: 2017-07-31T20:53:51+02:00
tags: go
---



This one-liner assigns a string to a slice of bytes:

```go
package main

func main() {

    var s string

    //...

    b := []byte(s)

    //...
}
```

I found this useful when using `ioutil.WriteFile`, which accepts a bytes slice as its `data` parameter:

> WriteFile func(filename string, data []byte, perm os.FileMode) error

e.g.:

```go
ioutil.WriteFile(filePath, []byte(content), 0755)
```
