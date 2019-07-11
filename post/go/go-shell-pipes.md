---
title: "Using Shell Pipes with Go"
date: 2017-07-29T11:04:59+02:00
tags: go
---

Being a good citizen in the command line means using pipes.

Using the vertical bar `|` we can pass the output of a command as an input of another command, and chain multiple commands to provide a unique output.

I have made 2 tutorials that use pipes as their input, building [gocowsay](/go-tutorial-cowsay) and [gololcat](/go-tutorial-lolcat), but I didn't describe in detail the process to get input from a pipe, so here's an article on this topic.

Here's an example:

```go
package main

import (
	"bufio"
	"fmt"
	"io"
	"os"
)

func main() {
	info, err := os.Stdin.Stat()
    if err != nil {
        panic(err)
    }

	if info.Mode()&os.ModeCharDevice != 0 || info.Size() <= 0 {
		fmt.Println("The command is intended to work with pipes.")
		fmt.Println("Usage: fortune | gocowsay")
		return
	}

	reader := bufio.NewReader(os.Stdin)
	var output []rune

	for {
		input, _, err := reader.ReadRune()
		if err != nil && err == io.EOF {
			break
		}
		output = append(output, input)
	}

	for j := 0; j < len(output); j++ {
		fmt.Printf("%c", output[j])
	}
}
```

Let's examine how this works. First interesting line:

```go
info, err := os.Stdin.Stat()
```

`os.Stdin`, like Stdout and Stderr, is an open [File](https://golang.org/pkg/os/#File). It points to the standard input file descriptor.

`Stat()` is a method of File that returns a [FileInfo](https://golang.org/pkg/os/#FileInfo) describing the file, providing information including mode and file size.

The next interesting piece is

```go
info.Mode()&os.ModeCharDevice != 0
```

`FileInfo.Mode()` returns the `uint32` mask that determines the file mode and permissions as a const (<https://golang.org/pkg/os/#FileMode>).

Usign a bitwise AND determines if the file mode is os.ModeCharDevice. This is a way to make sure that the file points to a `ModeCharDevice`, the Unix character device (terminal). Since the file points to `os.Stdin`, We're basically excluding the input being a pipe.

Bitwise returns 0 if the mode is _not_ the constant we pass. We could also check for

```go
info.Mode()&os.ModeCharDevice == os.ModeCharDevice
```

that's the same, but more readable.

If this is false, we have an additional check for

```go
info.Size() <= 0
```

which combined with the previous check, makes sure have an input pipe, and that actually contains some bytes.

We could also check for

```go
if info.Mode()&os.ModeNamedPipe != 0 {
	// we have a pipe input
}
```

and this will make sure the input comes from the pipe.

Next the program creates a reader

```go
reader := bufio.NewReader(os.Stdin)
```

[`bufio`](https://golang.org/pkg/bufio/) is a package that implements buffered I/O, basically wrapping `io.Reader` and `io.Writer`.

We ask it to give us a buffered reader from os.Stdin, using the default buffer size which is 4096 bytes.

`bufio.Reader` provides many methods to read data: `ReadByte`, `ReadBytes`, `ReadLine`, `ReadRune`, `ReadSlice`, `ReadString`.

The example uses `ReadRune` so it can add each rune read into the `var output []rune` slice, and handle [unicode](/unicode/) chars without any effort.

### Read more

- Named pipes: http://www.albertoleal.me/posts/golang-pipes.html