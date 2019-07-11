---
title: "Named Go returns parameters"
date: 2017-07-21T18:30:17+02:00
tags: go
---

In Go you can write functions that have named result parameters.

Two examples from [the spec](https://golang.org/ref/spec#Return_statements):

```go
func complexF3() (re float64, im float64) {
    re = 7.0
    im = 4.0
    return
}

func (devnull) Write(p []byte) (n int, _ error) {
    n = len(p)
    return
}
```

There are some many advantages on using this syntax.

You don't have to manually allocate the return variables, as having them named as result types, they are automatically initialized at their zero value for their type when the function begins.

Named return parameters do a very good job as implicit documentation: you know what the function is returning directly from its signature, as naming things help understand the code.

If there are multiple exit points from a function, you don't need to write all the parameters, just `return` (called _bare return_). You still _can_ list the returned values explicitly, and probably you should, to prevent having code hard to read. As suggested in [The Go Programming Language](https://gopl.io):

> [...] with many return statements and several results, bare returns can reduce code duplication, but they rarely make code easier to understand. [...] Bare returns are best used sparingly

An example:

```go
func something(n int) (ret int, m string, err error) {
    if n == 0 {
        err = errors.New("Houston, we have a problem!")
        return 0, "", err
    }

    ret = n + 100
    m = "Congratulations"

    return ret, m, err
}
```

or with bare returns:

```go
func something(n int) (ret int, m string, err error) {
    if n == 0 {
        err = errors.New("Houston, we have a problem!")
        return
    }

    ret = n + 100
    m = "Congratulations"

    return
}
```

In both cases the code is cleaner and more readable than

```go
func something(n int) (int, string, error) {
    var ret int
    var m string

    if n == 0 {
        err := errors.New("Houston, we have a problem!")
        return ret, m, err
    }

    ret = n + 100
    m = "Congratulations"

    return ret, m, nil
}
```

Beware the risk of shadowing a parameter with a new declaration inside the function.

So, when should you use them? When it makes sense to you in the overall design of a program. I'll let [The Go Programming Language](https://gopl.io) reply with a quote:

> [...] it's not always necessary to name multiple results solely for documentation. For instance, convention dictates that a final `bool` result indicates success; an `error` often needs no explanation.

---

Additional resources:

- <https://golang.org/doc/effective_go.html#named-results>
- <https://golang.org/ref/spec#Return_statements>
- <https://stackoverflow.com/questions/45239409/empty-return-in-func-with-return-value-in-golang>
