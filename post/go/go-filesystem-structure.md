---
title: "Filesystem Structure of a Go project"
date: 2017-07-23T18:30:17+02:00
tags: go
---

## Folder structure

Go projects are composed by **packages**. We call **commands** the packages that have the `main` identifier.

A project can have

- `1` package
- `n` packages
- `1` command
- `1` command and `1` package
- `n` commands and `1` package
- `1` command and `n` packages
- `n` commands and `n` packages

Depending on the nature of your project you need to organize the folder structure in a certain way.

### Some real world examples

Let's see some real world examples of this in the wild, here below. I took them from [Five suggestions for setting up a Go project](https://dave.cheney.net/2014/12/01/five-suggestions-for-setting-up-a-go-project) by Dave Cheney.

#### Example of a project with `1` package:

<https://github.com/kr/fs>

#### Example of a project with `n` packages

<https://github.com/pkg/term>

#### Example of a project with `1` command

<https://github.com/tools/godep>

#### Example of a project with `1` command and `1` package

<https://github.com/monochromegane/the_platinum_searcher>

#### Example of a project with `n` commands and `n` packages

<https://github.com/golang/tools>


### Conventions for file structure inside a project

From those examples we can tell these conventions:

If you have one command, it can live in a `main.go` file in the root of the project.

With more than one command, create a `cmd/` folder, and under this, create a folder with the name of the command. In each folder, ideally a `.go` file with the same name will contain the `main()` function, although it's not mandatory.

Packages go in their own folder, unless you just have one package.

## Filesystem location for installed packages

Any Go project can be installed by using `go get`. `go get` will install packages under `$GOPATH/src`. For example typing

```sh
go get github.com/kr/fs
```

will download and install the 1-package repo located at https://github.com/kr/fs, and it will put it under `$GOPATH/src/github.com/kr/fs`. We can just reference it in our programs using `import github.com/kr/fs`.

What if we type

```sh
go get github.com/tools/godep
```

instead? Remember, this is the one-command repository we listed before.

`go get` will download it like it did for `github.com/kr/fs`, and put it under `$GOPATH/src`, BUT since it's a command, it will also compile and create a `$GOPATH/bin/godep` binary.

Go commands are compiled to the name of the enclosing folder, in this case the folder was the root one, so it's `godep`. In the case of multiple commands, it will take the **last subfolder** name. E.g. an ideal `github.com/flaviocopes/tools/cmd/unzip` would be compiled to `unzip`. It does _not_ take the name of the file containing the `main()` function.

## Workspaces

Go has a quite unique concept of **workspace**. A workspace is the folder structure that `$GOPATH` points to. When you create a new workspace, add the `$GOPATH/bin` folder to your path as well. For example if you want to set your workspace to `~/go` (which by the ways is the default):

```sh
export GOPATH=~/go
export PATH=~/go/bin:$PATH
```

Now, any Go code you run will reference this folder. This allows you to create separate workspaces, although as stated [in the official docs](https://golang.org/doc/code.html#Organization),

> Go programmers typically keep all their Go code in a single workspace.

> Note that this differs from other programming environments in which every project has a separate workspace and workspaces are closely tied to version control repositories.

This is an example of a workspace, listed in the official docs:

```sh
    bin/
        hello                          # command executable
        outyet                         # command executable
    pkg/
        linux_amd64/
            github.com/golang/example/
                stringutil.a           # package object
    src/
        github.com/golang/example/
            .git/                      # Git repository metadata
        hello/
            hello.go               # command source
        outyet/
            main.go                # command source
            main_test.go           # test source
        stringutil/
            reverse.go             # package source
            reverse_test.go        # test source
        golang.org/x/image/
            .git/                  # Git repository metadata
        bmp/
            reader.go              # package source
            writer.go              # package source
        #... (many more repositories and packages omitted) ...
```

Knowing this, let's see..

## Where to place your commands and packages

When running commands using `go run`, you can have your project anywhere you like, but this is an approach useful only for quick testing.

You should create your programs inside the `$GOPATH/src` folder, with your unique namespace, e.g.

```sh
$GOPATH/src/github.com/flaviocopes/hello
```

When running (from anywhere in the system)

```sh
go install github.com/flaviocopes/hello
```

Go will compile and put the `hello` binary in `$GOPATH/bin`, ready to be run from anywhere in the system.

The same goes for packages, _except_ that when running `go install`, it will put the compiled package under `$GOPATH/pkg`.

## Reference

- <https://golang.org/doc/code.html#Organization>
- <https://dave.cheney.net/2014/12/01/five-suggestions-for-setting-up-a-go-project>
- <https://skife.org/golang/2013/03/24/go_dev_env.html>
- <https://stackoverflow.com/questions/14867452/what-is-a-sensible-way-to-layout-a-go-project>
- <https://medium.com/@benbjohnson/structuring-applications-in-go-3b04be4ff091>

