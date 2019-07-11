---
title: "Go Tags explained"
description: "How tags can add meta information to structs, and how you can take advantage"
date: 2016-12-01T11:04:59+02:00
tags: go
---

Tags are a way to attach additional information to a struct field.

The Go spec in the [Struct types definition](https://golang.org/ref/spec#Struct_types) defines tags as

> A field declaration may be followed by an optional string literal tag, which becomes an attribute for all the fields in the corresponding field declaration. An empty tag string is equivalent to an absent tag. The tags are made visible through a reflection interface and take part in type identity for structs but are otherwise ignored.

and provides an example:

```go
struct {
    x, y float64 ""  // an empty tag string is like an absent tag
    name string  "any string is permitted as a tag"
    _    [4]byte "ceci n'est pas un champ de structure"
}

// A struct corresponding to a TimeStamp protocol buffer.
// The tag strings define the protocol buffer field numbers;
// they follow the convention outlined by the reflect package.
struct {
    microsec  uint64 `protobuf:"1"`
    serverIP6 uint64 `protobuf:"2"`
}
```

## A real-world example

A common use-case for this is when unmarshaling JSON, as I explain in [JSON processing with Go](/go-json/).

In that post, the example

```go
type Member struct {
    Age       int `json:"age,string"`
}
```

tells `json.Unmarshal()` to put the `age` JSON property, a `string`, and put it in the `Age` field of `Member`, translating to an `int`. In this example, we pass `json` two informations, separated with a comma.

## Format of tags

Tags use the `key:"value"` format. It's not a strict rule, but a convention, which provides built-in parsing. In that example,we have only one key-value pair, but we could have more than one:

```go
type Member struct {
    Age       int `json:"age,string" xml:"the_age,string"`
}
```

The key by convention is the name of the package we want to target. In the above example, `encoding/json` and `encoding/xml`.

But tags can be used also by ourselves in our own libraries, they are not just reserved for the standard library.

## What are tags used for?

Different packages use tags for different reasons.

You'll see them used in encoding libs, like json, xml, bson, yaml, but also in ORM / database libs, and even [filling a struct with form data](http://godoc.org/github.com/gorilla/schema).

The following list was posted on [SO](https://stackoverflow.com/a/30889373/205039) and is quite comprehensive:

- `json     ` - used by the [`encoding/json`][11] package, detailed at [`json.Marshal()`][12]
- `xml      ` - used by the [`encoding/xml`][13] package, detailed at [`xml.Marshal()`][14]
- `bson     ` - used by [gobson][15], detailed at [`bson.Marshal()`][16]
- `protobuf ` - used by [`github.com/golang/protobuf/proto`][17], detailed in the package doc
- `yaml     ` - used by the [`gopkg.in/yaml.v2`][18] package, detailed at [`yaml.Marshal()`][19]
- `db` - used by the [`github.com/jmoiron/sqlx`][20] package
- `orm      ` - used by the [`github.com/astaxie/beego/orm`][21] package, detailed at [Models – Beego ORM][22]
- `gorm     ` - used by the [`github.com/jinzhu/gorm`][23] package, examples can be found in their doc: [Models][24]
- `datastore` - used by [`appengine/datastore`][25] (Google App Engine platform, Datastore service), detailed at [Properties][26]
- `schema   ` - used by [`github.com/gorilla/schema`][27] to fill a `struct` with HTML form values, detailed in the package doc
- `asn      ` - used by the [`encoding/asn1`][28] package, detailed at [`asn1.Marshal()`][29] and [`asn1.Unmarshal()`][30]

  [11]: https://golang.org/pkg/encoding/json/
  [12]: https://golang.org/pkg/encoding/json/#Marshal
  [13]: https://golang.org/pkg/encoding/xml/
  [14]: https://golang.org/pkg/encoding/xml/#Marshal
  [15]: https://labix.org/gobson
  [16]: http://godoc.org/gopkg.in/mgo.v2/bson#Marshal
  [17]: http://godoc.org/github.com/golang/protobuf/proto
  [18]: https://godoc.org/gopkg.in/yaml.v2
  [19]: https://godoc.org/gopkg.in/yaml.v2#Marshal
  [20]: https://godoc.org/github.com/jmoiron/sqlx
  [21]: https://godoc.org/github.com/astaxie/beego/orm
  [22]: https://beego.me/docs/mvc/model/overview.md
  [23]: https://github.com/jinzhu/gorm
  [24]: http://jinzhu.me/gorm/models.html
  [25]: https://cloud.google.com/appengine/docs/go/datastore/reference
  [26]: https://cloud.google.com/appengine/docs/go/datastore/reference#hdr-Properties
  [27]: http://godoc.org/github.com/gorilla/schema
  [28]: https://golang.org/pkg/encoding/asn1/
  [29]: https://golang.org/pkg/encoding/asn1/#Marshal
  [30]: https://golang.org/pkg/encoding/asn1/#Unmarshal

There are many other usages in the wild. For example [mcuadros/go-defaults](https://github.com/mcuadros/go-defaults) use s it to set default values for struct fields, and [asaskevich/govalidator](https://github.com/asaskevich/govalidator) allows to add tags that determine validation (that's just one possible way of validating, [alternatives exist](https://github.com/go-ozzo/ozzo-validation)).

[fatih/gomodifytags](https://github.com/fatih/gomodifytags) allows to edit tags at runtime,

## Using tags in your code

To use tags in your own code, you can use the [`reflect` package](https://golang.org/pkg/reflect/).

Let's try getting `age` in a Member struct. The following code

```go
package main

import (
    "fmt"
    "reflect"
)

type Member struct {
    Age int `something:"age"`
}

func main() {
    member := Member{34}
    t := reflect.TypeOf(member)
    field := t.Field(0)
    //field, _ := t.FieldByName("Age") //alternative
    fmt.Print(field.Tag.Get("something"))
}
```

[play](https://play.golang.org/p/LQMI_14SHr)

will print "something", thanks to adhering to the `key:"value"` format for our tag.


