---
title: "Using environment variables in Go"
date: 2017-08-15T15:46:52+02:00
tags: go
---

Parsing environment variables with Go is simple, thanks to the standard library `os` package.

[`os.Getenv()`](https://golang.org/pkg/os/#Getenv) **gets** an environment variable. It's not possible to determine not set or empty. Use `os.LookupEnv()` to be able to do that.

```go
name := os.Getenv("NAME")
```

[`os.Setenv()`](https://golang.org/pkg/os/#Setenv) **sets** an environment variable.

```go
os.Setenv("NAME", "Flavio")
```

[`os.Unsetenv()`](https://golang.org/pkg/os/#Unsetenv) **unsets** an environment variable.

```go
os.Unsetenv("NAME")
```

[`os.Clearenv()`](https://golang.org/pkg/os/#Clearenv) **unsets all** environment variables.

```go
os.Clearenv()
```

[`os.Environ()`](https://golang.org/pkg/os/#Environ) returns a **slice** of strings containing all the environment variables in `key=value` format.

```go
vars := os.Environ()
```

[`os.ExpandEnv()`](https://golang.org/pkg/os/#ExpandEnv) given a string, **expands $VAR** environment variables entries to the corresponding value.

```go
s := os.ExpandEnv("$NAME is italian")
```

[`os.LookupEnv()`](https://golang.org/pkg/os/#LookupEnv) returns the value of the environment variable in its first parameter if set, otherwise the second parameter is false. Allows to distinguish unset from empty value.

```go
name, ok := os.LookupEnv("NAME")
```
