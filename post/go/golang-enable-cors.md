---
title: "Enabling CORS on a Go Web Server"
date: 2017-08-16T16:04:59+02:00
tags: go
---

[CORS](/cors/) stands for _Cross Origin Resource Sharing_ and it's a very handy way to make an API accessible by [JavaScript](/javascript/) in-browser client-side code.

If you are looking for a simple, quick way to enable CORS in localhost, or to open your API to anyone in the world, use:

```go
func handler(w http.ResponseWriter, req *http.Request) {
    // ...
	enableCors(&w)
    // ...
}

func enableCors(w *http.ResponseWriter) {
	(*w).Header().Set("Access-Control-Allow-Origin", "*")
}
```

This does not provide any kind of control or fine tuning, and it's intended for testing purposes only. Take a look at <https://github.com/rs/cors> for a more advanced setup.

## Handling pre-flight OPTIONS requests

CORS does pre-flight requests sending an OPTIONS request to any URL, so to handle a POST request you first need to handle an OPTIONS request to that same URL.

On GET endpoints this is not an issue, but it is for POST and PUT and DELETE requests.

How?

```go
func setupResponse(w *http.ResponseWriter, req *http.Request) {
	(*w).Header().Set("Access-Control-Allow-Origin", "*")
    (*w).Header().Set("Access-Control-Allow-Methods", "POST, GET, OPTIONS, PUT, DELETE")
    (*w).Header().Set("Access-Control-Allow-Headers", "Accept, Content-Type, Content-Length, Accept-Encoding, X-CSRF-Token, Authorization")
}

func indexHandler(w http.ResponseWriter, req *http.Request) {
	setupResponse(&w, req)
	if (*req).Method == "OPTIONS" {
		return
	}

    // process the request...
}
```

Again, this is intended for private use CORS only. Public use needs to be restricted.