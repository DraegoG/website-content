---
title: Solving the "does not support indexing" error in a Go program
date: 2017-08-03T20:04:59+02:00
tags: go
---

If you're reading this post you're probably searching on Google how to solve this problem: you're passing a pointer to a `slice` or `map` in a function, and when referencing an item with `*variable[0]`, you get that error.

## How do I solve it?

The solution is simple: instead of using

```go
*variable[0]
```

use

```go
(*variable)[0]
```

## Why am I getting this weird error? :thinking:

`*variable[0]` is interpreted by the Go compiler as `*(variable[0])`. So what you're telling the compiler to do is, get the first element in the slice, or the map item with key 0, and dereference that pointer.

This explains the error: `variable` in that context is a pointer, not a value, so you cannot get the [0] item of a pointer to an address, you need to dereference it first to get the value, which is what I think you are trying to do in the first place.