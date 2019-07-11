---
title: "List the files in a folder with Go"
date: 2017-07-30T11:30:17+02:00
tags: go
---

In this article I explain how to get a list of files inside a folder on the filesystem, a task also called **tree traversing**, with Go.

There are two handy stdlib functions that you can use depending on your goal.

I list 3 ways: using `filepath.Walk`, `ioutil.ReadDir` or `os.File.Readdir`.

## Using `filepath.Walk`

The `path/filepath` stdlib package provides the handy Walk function. It automatically scans subdirectories, though, so make sure this is what you actually want.

Usage is very simple:

```go
package main

import (
    "fmt"
    "os"
    "path/filepath"
)

func main() {
    var files []string

    root := "/some/folder/to/scan"
    err := filepath.Walk(root, func(path string, info os.FileInfo, err error) error {
        files = append(files, path)
        return nil
    })
    if err != nil {
        panic(err)
    }
    for _, file := range files {
        fmt.Println(file)
    }
}
```

[`filepath.Walk`](https://golang.org/pkg/path/filepath/#Walk) accepts a string pointing to the root folder, and a [`WalkFunc`](https://golang.org/pkg/path/filepath/#WalkFunc), a function type with signature

```go
type WalkFunc func(path string, info os.FileInfo, err error) error
```

This function is called for each iteration of the folder scan.

The `info` variable of type [`os.FileInfo`](https://golang.org/pkg/os/#FileInfo) is important because we can get many information on the current file: the name, size, mode, modification time, if it's a folder or a file, and the underlying data source.

For example we could avoid processing folders by adding

```go
if info.IsDir() {
    return nil
}
```

You can exclude (or include) files to the slice based on their extension, by using [`filepath.Ext`](https://golang.org/pkg/path/filepath/#Ext) and passing the file path:

```go
if filepath.Ext(path) == ".dat" {
    return nil
}
```

We could store the file name instead of the file path using

```go
files = append(files, info.Name())
```

And we could also define the `WalkFunc` in a separate **closure**. We just need to pass a pointer to `files` in `visit`:

```go
package main

import (
    "fmt"
    "log"
    "os"
    "path/filepath"
)

func visit(files *[]string) filepath.WalkFunc {
    return func(path string, info os.FileInfo, err error) error {
        if err != nil {
            log.Fatal(err)
        }
        *files = append(*files, path)
        return nil
    }
}

func main() {
    var files []string

    root := "/some/folder/to/scan"
    err := filepath.Walk(root, visit(&files))
    if err != nil {
        panic(err)
    }
    for _, file := range files {
        fmt.Println(file)
    }
}
```

## Using `ioutil.ReadDir`

`filepath.Walk` is handy but scans subfolders too, by default, which might not be what you want.

The Go stdlib also provides [`ioutil.ReadDir`](https://golang.org/pkg/io/ioutil/#ReadDir)

```go
func ReadDir(dirname string) ([]os.FileInfo, error)
```

> ReadDir reads the directory named by dirname and returns a list of directory entries sorted by filename.

and here's an example from the docs. `ioutil.ReadDir` takes a folder path as a string and returns a slice of [`os.FileInfo`](https://golang.org/pkg/os/#FileInfo), which we described above.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "log"
)

func main() {
    files, err := ioutil.ReadDir(".")
    if err != nil {
        log.Fatal(err)
    }

    for _, file := range files {
        fmt.Println(file.Name())
    }
}
```

## Using `os.File.Readdir`

Internally, `ioutil.ReadDir` is implemented as

```go
// ReadDir reads the directory named by dirname and returns
// a list of directory entries sorted by filename.
func ReadDir(dirname string) ([]os.FileInfo, error) {
    f, err := os.Open(dirname)
    if err != nil {
        return nil, err
    }
    list, err := f.Readdir(-1)
    f.Close()
    if err != nil {
        return nil, err
    }
    sort.Slice(list, func(i, j int) bool { return list[i].Name() < list[j].Name() })
    return list, nil
}
```

as you can see it scans `dirname` and sorts the files by name. If you don't need sorting you can as well use

```go
package main

import (
    "fmt"
    "log"
    "os"
)

func main() {
    dirname := "."

    f, err := os.Open(dirname)
    if err != nil {
        log.Fatal(err)
    }
    files, err := f.Readdir(-1)
    f.Close()
    if err != nil {
        log.Fatal(err)
    }

    for _, file := range files {
        fmt.Println(file.Name())
    }
}
```

