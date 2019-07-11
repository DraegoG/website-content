---
title: "Accessing HTTP POST parameters in Go"
date: 2017-08-30T09:07:09+02:00
tags: go
---

I ran into a little issue as I tried to POST to a Go backend using [Axios](/axios/) but I could not get the parameters I was sending.

I was doing this:

```go
func handleReq(w http.ResponseWriter, req *http.Request) {
	err := req.ParseForm()
	if err != nil {
		panic(err)
	}
	v := req.Form
	owner := req.Form.Get("owner")
	name := req.Form.Get("name")
    //...
}
```

but the two parameters I was looking for were not available. Why?

Turns out that I was assuming Axios sent the parameters using `Content-Type:application/x-www-form-urlencoded` but by default it's using `Content-Type:application/json`.

> Note: you can configure it to use `application/x-www-form-urlencoded`, check <https://github.com/axios/axios#using-applicationx-www-form-urlencoded-format>

This means that to access the parameters I need to decode them using [json.Decoder](https://golang.org/pkg/encoding/json/#Decoder).

Here is some sample code that does the trick:

```go
type myData struct {
	Owner string
	Name  string
}

func handleAddNewRepo(w http.ResponseWriter, req *http.Request) {
	decoder := json.NewDecoder(req.Body)

	var data myData
	err := decoder.Decode(&data)
	if err != nil {
		panic(err)
	}

	owner := data.Owner
	name := data.Name
    //...
}
```