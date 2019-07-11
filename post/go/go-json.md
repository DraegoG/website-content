---
title: "JSON processing with Go"
description: "The basics of marshaling and unmarshaling JSON"
date: 2017-03-07T11:04:59+02:00
tags: go
---

JSON stands for [JavaScript](/javascript/) Object Notation, and it's a very handy way of exchanging structured data. And it's very popular, especially when interacting with APIs.

Go has top-level support for JSON in its standard library, with [the `encoding/json` package](https://golang.org/pkg/encoding/json/).

Compared to loosely typed languages, decoding JSON is more complicated. In JavaScript, all you need to do is `JSON.parse()`. Python has `json.loads()`, and PHP has `json_decode()`. They just dump values without problems, but being Go strongly typed, you need to do a little bit more work to match the types.

JSON has 3 basic types: **booleans**, **numbers**, **strings**, combined using **arrays** and **objects** to build complex structures.

Go's terminology calls **marshal** the process of generating a JSON string from a data structure, and **unmarshal** the act of parsing JSON to a data structure.

A JSON string

```go
input := `{"firstname": "Bill", "surname": "Gates"}`
```

## Unmarshal JSON

Here is a JSON example taken from [Mozilla's MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)

```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

How can we parse it into a Go data structure? We need a matching data structure, of course. We have 5 basic types, and an array of objects. Let's start with the basic types:

```go
type squad struct {
    SquadName string
    HomeTown string
    Formed int
    SecretBase string
    Active bool
}
```

We need to define the JSON as a `[]byte`, like this:

```go
input := []byte(`
    {
        "squadName": "Super hero squad",
        [...]
    }
`)
```

And we can unmarshal the JSON to a squad instance:

```go
s := squad{}
err := json.Unmarshal(input, &s)
if err != nil {
    panic(err)
}
fmt.Printf("%v", s)
```

This will print

```sh
{Super hero squad Metro City 2016 Super tower true}
```

[play](https://play.golang.org/p/wljXmfAeG4)

Notice how we don't have any error complaining about the missing match between JSON values and our struct, they are ignored.

Let's make sure json.Unmarshal() will get us all the fields, with:

```go
type squad struct {
	SquadName  string
	HomeTown   string
	Formed     int
	SecretBase string
	Active     bool
	Members    []Member
}

type Member struct {
	Name           string
	Age            int
	SecretIdentity string
	Powers         []string
}
```
[play](https://play.golang.org/p/i1mYcTi4ZZ)

Remember to have public (uppercase) properties in your structs.

### Renaming JSON field names

In this case, all was fine because the JSON had compatible file names. What if you want to map the JSON to other fields in your struct?

For example, what if the Member name is passed as `member_name`, but you want it to be stored in `Name` instead?

Use this syntax:

```go
type Member struct {
	Name string `json:"member_name"`
}
```

### Ignoring JSON fields

Use this syntax:

```go
type Member struct {
	Name string `json:"-"`
}
```

and Name field will be ignored when marshaling/unmarshaling.

### Converting JSON field types

You can use tags to annotate the type that the JSON will be converted to:

```go
type Member struct {
    Age       int `json:"age,string"`
}
```

The Member struct has an `Age` property that's represented as an `int`. What if you want it to be a `string` instead, but JSON passes an `int`?

Use the type annotation:

```go
type Member struct {
    Age       json.Number `json:"age,Number"`
}
```

The Number type is an alias for `string`.

Learn more about tags in [Go Tags explained](/go-tags)

## Marshal JSON

We might now want to build a JSON string from our data structures. For example, this could be a program that takes an country code, and returns the corresponding country details in JSON format.

```go
package main

import (
	"encoding/json"
	"fmt"
)

type country struct {
	Name string
}

func main() {
	country_code := "US"

	the_country := country{}

	switch country_code {
	case "US":
		the_country.Name = "United States"
	}

	c, err := json.Marshal(the_country)
	if err != nil {
		panic(err)
	}

	// c is now a []byte containing the encoded JSON
	fmt.Print(string(c))
}
```
[play](https://play.golang.org/p/gRjH7uA1m-)

When executed, this program will print `{"Name":"United States"}`.

`json.Marshal()` returns a `[]byte`, so we must cast it to string when passing it to `fmt.Print()`, otherwise you'll see a list of apparently meaningless numbers (but they are meaningful, as they are the actual bytes that compose the string).

`json.Marshal()` will correctly process basic and composit types like slices and maps.

## Read more

Read more [on the Go blog](https://blog.golang.org/json-and-go) and in [the `encoding/json` package doc](https://golang.org/pkg/encoding/json/)