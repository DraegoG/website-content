---
title: "Using Command Line Flags in Go"
date: 2017-07-25T09:07:09+02:00
tags: go
---

There are many ways to process CLI flags using Go. The first option is to not use any library at all, and inspect `os.Args`. The second option is to use the standard library [`flag`](https://golang.org/pkg/flag/) package. The third option is to use one of the many 3rd party CLI libs out there, like [Cobra](https://github.com/spf13/cobra).

Let's talk about the second option: using the standard library `flag`, as it offers many benefits over raw parsing of `os.Args` and it's built-in.

Add `import "flag"` to the import section of your package, and it's ready to use.

To accept an `int` parameter type:

```go
func Int(name string, value int, usage string) *int

var count = flag.Int("count", 5, "the count of items")
fmt.Println("count value ", *count)
```

The first parameter is the flag name as used in the CLI command, the second parameter is the default value, and the third is the description.

An alternative syntax is provided by `flag.IntVar()`:

```go
func IntVar(p *int, name string, value int, usage string)

var count int
flag.IntVar(&count, "count", 5, "the count of items")
fmt.Println("count value ", count)
```

Here the parameters are shifted, and the first parameter is the variable reference.

The main difference is that in the first case, you get a pointer. In the second case, you get a value.

`flag` provides many functions to parse different flag types, you'll need to use a different one for each type you want to accept:

```go
func Bool(name string, value bool, usage string) *bool
func BoolVar(p *bool, name string, value bool, usage string)
func Duration(name string, value time.Duration, usage string) *time.Duration
func DurationVar(p *time.Duration, name string, value time.Duration, usage string)
func Float64(name string, value float64, usage string) *float64
func Float64Var(p *float64, name string, value float64, usage string)
func Int(name string, value int, usage string) *int
func Int64(name string, value int64, usage string) *int64
func Int64Var(p *int64, name string, value int64, usage string)
func IntVar(p *int, name string, value int, usage string)
func String(name string, value string, usage string) *string
func StringVar(p *string, name string, value string, usage string)
func Uint(name string, value uint, usage string) *uint
func Uint64(name string, value uint64, usage string) *uint64
func Uint64Var(p *uint64, name string, value uint64, usage string)
func UintVar(p *uint, name string, value uint, usage string)
```

Passing the wrong type for a flag will raise an error, halt the program, and the required usage will be printed to the user.

As an example, here's how you parse a string:

```go
var description = flag.String("description", "default value", "the description of the flag")
```

### Flags syntax

How do you set flag? Simple: attach `-flagname` to your CLI command, with 4 alternative but equivalent syntaxes:

```sh
-count=x
-count x
--count=x
--count x
```

You can pass as many flags as you want to a command, but the first time `flag` does not recognize a flag, it will stop parsing the additional ones. This means that flags must all go at the beginning, if you have non-flag parameters as well.

### Parse the flags

After defining all your flags, you need to call

```go
flag.Parse()
```

to actually parse them.

### Boolean flags

Boolean flags can be set just by adding `-count`, which makes the boolean flag get the `true` value. To set a `false` value, use `-count=false`. Any of those values are valid for boolean flags: `1, 0, t, f, T, F, true, false, TRUE, FALSE, True, False`.

### Short alternative

Many times in the real world you'll see CLI apps accepting a flag with a descriptive name, and the same flag with a letter abbreviation. You can do it by providing 2 flag handlers:

```go
var gopherType string

func init() {
    const (
        defaultGopher = "pocket"
        usage         = "the variety of gopher"
    )
    flag.StringVar(&gopherType, "gopher_type", defaultGopher, usage)
    flag.StringVar(&gopherType, "g", defaultGopher, usage+" (shorthand)")
}
```

### Parsing non-flag parameters

The `flag` package provides methods to also parse non-flag parameters.

```go
flag.Args()
```

returns a slice of strings with the parameters not parsed as flags.

### Forcing a flag as required

The `flag` package does not provide a built-in solution for this problem. You need to manage this case yourself:

```go
// [...]
flag.Parse()

if *count == "" {
    flag.PrintDefaults()
    os.Exit(1)
}
```

### More advanced topics

This is an introductory article. You can go into more in-depth topics from here, like implementing subcommands and definining your own flag types. See <https://blog.komand.com/build-a-simple-cli-tool-with-golang> for more advanced usage of the CLI.

## Reference

- <https://golang.org/pkg/flag/>
- <https://thenewstack.io/cli-command-line-programming-with-go/>
- <https://blog.komand.com/build-a-simple-cli-tool-with-golang>