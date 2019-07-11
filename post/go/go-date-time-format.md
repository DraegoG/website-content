---
title: "Go Date and Time Formatting"
description: "Learn how to format a date in Go, using format constants or a custom format"
date: 2017-01-16T13:53:51+02:00
tags: go
---

In Go, the current time can be determined using `time.Now()`, provided by the [`time` package](https://golang.org/pkg/time).

```go
t := time.Now()
```

This will print the system local time. Want UTC instead? append `.UTC()`:

The time can be formatted using the `time.Format()` method:

```go
t := time.Now().UTC()
```

Want the timestamp?

```go
t := time.Now().Unix()
```

## Use a custom format

An example of formatting with a custom format is:

```go
fmt.Println(t.Format("2006-01-02 15:04:05"))
```

That `2006-01-02 15:04:05` string looks strange, isn't it? It's not like it's 2006 now! Bu it will print (at the time of writing) `2017-01-16 12:53:51`

If you're new to Go, this will sound _very_ strange.

Here's the explanation: Go's time formatting is unique and different than what you would do in other languages. Instead of having a conventional format to print the date, Go uses the reference date `20060102150405` which seems meaningless but actually has a reason, as it's `1 2 3 4 5 6` in the Posix `date` command:

```sh
Mon Jan 2 15:04:05 -0700 MST 2006
0   1   2  3  4  5              6
```

The timezone in the middle would have been the `7` (not really sure why they didn't pick `Mon Jan 2 03:04:05 -0600 MST 2007`, by the way)

Interesting historical reference: https://github.com/golang/go/issues/444

## Use a format constants

Go provides in the `time` package some handy constants for commonly used formats:

```go
const (
        ANSIC       = "Mon Jan _2 15:04:05 2006"
        UnixDate    = "Mon Jan _2 15:04:05 MST 2006"
        RubyDate    = "Mon Jan 02 15:04:05 -0700 2006"
        RFC822      = "02 Jan 06 15:04 MST"
        RFC822Z     = "02 Jan 06 15:04 -0700" // RFC822 with numeric zone
        RFC850      = "Monday, 02-Jan-06 15:04:05 MST"
        RFC1123     = "Mon, 02 Jan 2006 15:04:05 MST"
        RFC1123Z    = "Mon, 02 Jan 2006 15:04:05 -0700" // RFC1123 with numeric zone
        RFC3339     = "2006-01-02T15:04:05Z07:00"
        RFC3339Nano = "2006-01-02T15:04:05.999999999Z07:00"
        Kitchen     = "3:04PM"
        // Handy time stamps.
        Stamp      = "Jan _2 15:04:05"
        StampMilli = "Jan _2 15:04:05.000"
        StampMicro = "Jan _2 15:04:05.000000"
        StampNano  = "Jan _2 15:04:05.000000000"
)
```

You can use them like this:

```go
t := time.Now()
fmt.Println(t.Format(time.ANSIC))
```