---
title: "Measuring execution time in a Go program"
date: 2017-08-04T16:04:59+02:00
tags: go
---

A common operation when developing a Go application, or benchmarking it to find ways to improve it, is benchmarking a function execution time. I introduced the topic of [CPU and memory profiling in Go](/golang-profiling/) already, but this is different and more suited to ad-hoc function execution time measurement.

## Determine the time interval between two expressions: use `time.Since`

[`time.Since`](https://golang.org/pkg/time/#Since) is a function provided by the `time` standard library package that takes a [`Time`](https://golang.org/pkg/time/#Time) value, computes the difference with the current time, and returns a [`Duration`](https://golang.org/pkg/time/#Duration) value, which is an int64 type with a `String()` method attached, which provides a human friendly notation for the time computed.

```go
import (
    "fmt"
    "time"
)

func main() {
    start := time.Now()

    //... do something

    fmt.Println(time.Since(start))
}
```

Internally, `time.Since` is a shorthand for  `time.Now().Sub(t)`.

### Using `defer` to measure time inside a function

You can abstract this by using `defer`:

```go
package main

import (
    "log"
    "time"
)

func runningtime(s string) (string, time.Time) {
    log.Println("Start:	", s)
    return s, time.Now()
}

func track(s string, startTime time.Time) {
    endTime := time.Now()
    log.Println("End:	", s, "took", endTime.Sub(startTime))
}

func execute() {
    defer track(runningtime("execute"))
    time.Sleep(3 * time.Second)
}

func main() {
    execute()
}
```


## Benchmark a function performance by running it multiple times: use the `testing` package

Here is a simple library I wrote, that counts the number of runes in a string.

> runecount.go

```go
package runecount

import "unicode/utf8"

func RuneCount(s string) int {
    return len([]rune(s))
}

func RuneCount2(s string) int {
    return utf8.RuneCountInString(s)
}
```

Which of the two ways to count the runes in a string is faster? We find out by writing a benchmark. Benchmarks live in the `*_test.go` file, like regular tests, and can stay in live with testing methods, that start with `Test*`, but they start with `Benchmark*` instead:

> runecount_test.go

```go
package runecount

import "testing"

func BenchmarkRuneCount(b *testing.B) {
    s := "Gophers are amazing 😁"
    for i := 0; i < b.N; i++ {
        RuneCount(s)
    }
}
func BenchmarkRuneCount2(b *testing.B) {
    s := "Gophers are amazing 😁"
    for i := 0; i < b.N; i++ {
        RuneCount2(s)
    }
}
```

I run this by executing, in the same folder where the files are located:

```bash
go test -bench=.
```

This causes all the benchmarks to run. I got just a single file, but in case you have many, you can specify which file to run.

Each benchmark runs the loop passing the b.N variable, which is automatically determined by the benchmark runner, until the average is stable enough to determine a result.

This is the output I get on my Mac:

```bash
# flavio @ Flavios-MacBook-Pro in ~/go/src/github.com/flaviocopes/snippets/benchmark on git:master x [18:32:26]
$ go test -bench=.
BenchmarkRuneCount-2            20000000               115 ns/op
BenchmarkRuneCount2-2           30000000                44.1 ns/op
PASS
ok      github.com/flaviocopes/snippets/benchmark       3.812s
```

`20000000` and `30000000` are the number of operations run.

The command returns the benchmark results: it ran 20M times `RuneCount()`, which took on average 163 nanoseconds, and then it ran 30M times `RuneCount2()`, which took on average 74.2 nanoseconds per each iteration.

So `Benchmark1`, which runs `RuneCount()`, is 2x slower than `RuneCount2()`, that uses the built-in [`utf8.RuneCountInString`](https://golang.org/pkg/unicode/utf8/#RuneCountInString) function. No surprise here, as `utf8.RuneCountInString` is highly optimized for this specific task.

---

Instead of using `go test`, you can also call `testing.Benchmark` from a command:

```go
package main

import (
    "fmt"
    "testing"
    "runecount"
)

func BenchmarkRuneCount(b *testing.B) {
    s := "Gophers are amazing 😁"
    for i := 0; i < b.N; i++ {
        RuneCount(s)
    }
}
func BenchmarkRuneCount2(b *testing.B) {
    s := "Gophers are amazing 😁"
    for i := 0; i < b.N; i++ {
        RuneCount2(s)
    }
}

func main() {
    fmt.Println(testing.Benchmark(BenchmarkRuneCount))
    fmt.Println(testing.Benchmark(BenchmarkRuneCount2))
}
```

## Where to read more

- <https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go>
- <http://www.soroushjp.com/2015/01/27/beautifully-simple-benchmarking-with-go/>
