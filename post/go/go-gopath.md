---
title: "GOPATH Explained"
date: 2017-07-26T11:04:59+02:00
tags: go
---

As written in [How to Write Go Code](https://golang.org/doc/code.html#Organization),

> Go programmers typically keep all their Go code in a single workspace.

> A workspace contains many version control repositories (managed by Git, for example).

> Each repository contains one or more packages.

The `GOPATH` environment variable specifies the location of your workspace. That's where you find the Go tools, where you develop and where you install 3rd party packages and binaries.

As of Go 1.8, if you don't set a `GOPATH`, the default will be used. In older releases had to set it explicitly, but for ease of use, a default has been introduced.
By default the value of `GOPATH` is

- `$HOME/go` on Unix-like systems
- `%USERPROFILE%\go` on Windows

This means that on macOS all your Go code will be put in the `/go` folder in your home directory.

This is the most common setup, but you might also choose to use your home directory as `GOPATH`.

Libraries installed using `go get` will be put in `$GOPATH/src`

Commands installed using `go get` will be put in `$GOPATH/bin`

Speaking of commands, you need to add `$GOPATH/bin` to your `PATH` to execute any binary installed in `$GOPATH/bin`, or you need to type `$GOPATH/bin/the-command`. Add this to your `~/.bash_profile` or `~/.zshrc` (or whatever shell you use) on *nix:

```sh
export PATH=$GOPATH/bin:$PATH
```

A quick way to know what is your current `GOPATH` is running

```sh
go env GOPATH
```

Changing the GOPATH is easy, add this to your shell config file:

```sh
export GOPATH=$HOME/another-go-path
```

([Here's how to set the PATH or GOPATH on Windows](https://github.com/golang/go/wiki/SettingGOPATH#windows))

### References

<https://github.com/golang/go/wiki/SettingGOPATH>
<https://golang.org/doc/code.html#GOPATH>
<https://github.com/golang/go/wiki/GOPATH>