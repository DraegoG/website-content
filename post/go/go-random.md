---
title: "Generating random numbers and strings in Go"
date: 2017-07-22T20:04:59+02:00
tags: go
---

While [completely random is not really possible](https://www.youtube.com/watch?v=sMb00lz-IfE), we still can have pseudorandom numbers on computers.

We can have _regular_ pseudorandom numbers, and _cryprographically secure_ pseudorandom numbers.

Let's see how to that in Go.

## Pseudorandom numbers

The [`math/rand` package](https://golang.org/pkg/math/rand/) provided by the Go Standard Library gives us [pseudo-random number generators (PRNG)](https://en.wikipedia.org/wiki/Pseudorandom_number_generator), also called _deterministic random bit generators_.

As with all pseudo number generators, any number generated through `math/rand` is **not really random** by default, as being deterministic **it will always print the same value each time**.

As an example, try running this code which introduces [`rand.Intn(n)`](https://golang.org/pkg/math/rand/#Rand.Intn), which returns a random number between `0` and `n - 1`.

```go
package main

import (
    "fmt"
    "math/rand"
)

func main() {
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
}
```

[playground](https://play.golang.org/p/-HsFj0sqWD)

You'll always see the same sequence every time you run the program. The random number changes inside the program, but every time you run it, you'll get the same output:

```sh
11
27
17
29
1
```

This is because by default the seed is always the same, the number `1`. To actually get a random number, you need to provide a unique [seed](https://en.wikipedia.org/wiki/Random_seed) for your program. You really want to not forget seeding, and instead properly seed our pseudonumber generator. How?

Use `rand.Seed()` before calling any `math/rand` method, passing an `int64` value. You just need to seed once in your program, not every time you need a random number. The most used seed is the current time, converted to `int64` by [UnixNano](https://golang.org/pkg/time/#Time.UnixNano) with `rand.Seed(time.Now().UnixNano())`:

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
    fmt.Println(rand.Intn(30))
}
```

Remember that due to its sandboxing, the Go Playground always begins with the same time, so this code won't work as expected. Try it on a real environment, and the numbers that previosly didn't change, they will now print differently each time you run the program.

Some common examples are listed below for ease of reuse:

### Generate a random integer

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

// Returns an int >= min, < max
func randomInt(min, max int) int {
    return min + rand.Intn(max-min)
}

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(randomInt(1, 11)) //get an int in the 1...10 range
}
```

### Generate a random string

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

// Returns an int >= min, < max
func randomInt(min, max int) int {
    return min + rand.Intn(max-min)
}

// Generate a random string of A-Z chars with len = l
func randomString(len int) string {
    bytes := make([]byte, len)
    for i := 0; i < len; i++ {
        bytes[i] = byte(randomInt(65, 90))
    }
    return string(bytes)
}

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(randomString(10)) // print 10 chars
}
```

Will return 10 chars in uppercase format. Change

```go
bytes[i] = byte(randomInt(65, 90))
```

to

```go
bytes[i] = byte(randomInt(97, 122))
```

for just lowercase.

If you instead want to have a pool of specific chars to pick from, use

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

var pool = "_:$%&/()"

// Generate a random string of A-Z chars with len = l
func randomString(l int) string {
    bytes := make([]byte, l)
    for i := 0; i < l; i++ {
        bytes[i] = pool[rand.Intn(len(pool))]
    }
    return string(bytes)
}

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(randomString(1000))
}
```

Change `len(pool)` to `utf8.RuneCountInString(pool)` if you use non-ascii strings, as `len()` counts the bytes, but not all chars take just one byte in Unicode - see <https://stackoverflow.com/questions/12668681/how-to-get-the-number-of-characters-in-a-string>.

### Generate a random array of integers

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func randomArray(len int) []int {
    a := make([]int, len)
    for i := 0; i <= len-1; i++ {
        a[i] = rand.Intn(len)
    }
    return a
}

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(randomArray(10))
}
```

## Crypto-level random numbers

Go also provides a [Cryptographically secure pseudorandom number generator (CSPRNG)](https://en.wikipedia.org/wiki/Cryptographically_secure_pseudorandom_number_generator) in the standard library package [`crypto.rand`](https://godoc.org/crypto/rand)

So you might question, why should I even use the pseudo-number random generator library provided by `math/rand` instead? Well, it depends on the use case. `math/rand` is **much faster** for applications that don't need crypto-level or security-related random data generation. `crypto.rand` is suited for secure and crypto-ready usage, but it's slower.

What it should be used for? For example, generating passwords, CSRF tokens, session keys, or anything remotely related to security.

It does not rely on the current time, like we did in the previous examples in `math/rand`, but instead it uses the operating system CSPRNG APIs: the CryptGenRandom API on Windows, and `/dev/urandom/` on all the others (Linux, OSX, *nix)

You get 256 random bytes directly with

```go
package main

import (
    "crypto/rand"
    "fmt"
)

func main() {
    key := [256]byte{}
    _, err := rand.Read(key[:])
    if err != nil {
        panic(err)
    }
    fmt.Println(key)
}
```

I'm taking a code sample from [Matt Silverlock](https://elithrar.github.io/article/generating-secure-random-numbers-crypto-rand/): you can make it more general and create a random bytes generation function

```go
// GenerateRandomBytes returns securely generated random bytes.
// It will return an error if the system's secure random
// number generator fails to function correctly, in which
// case the caller should not continue.
func GenerateRandomBytes(n int) ([]byte, error) {
    b := make([]byte, n)
    _, err := rand.Read(b)
    // Note that err == nil only if we read len(b) bytes.
    if err != nil {
        return nil, err
    }

    return b, nil
}
```

and using this, a random string generation function,

```go
// GenerateRandomString returns a URL-safe, base64 encoded
// securely generated random string.
// It will return an error if the system's secure random
// number generator fails to function correctly, in which
// case the caller should not continue.
func GenerateRandomString(s int) (string, error) {
    b, err := GenerateRandomBytes(s)
    return base64.URLEncoding.EncodeToString(b), err
}
```