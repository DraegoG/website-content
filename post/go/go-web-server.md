---
title: "The basics of a Go Web Server"
date: 2016-07-16T13:53:51+02:00
tags: go
---

Go is a networking oriented programming language, and as a matter of fact the standard library has a very powerful `net/http` module, and the "The Go Programming Language" book by Donovan and Kernighan has a web server example **in the first chapter**:

```go
// Copyright © 2016 Alan A. A. Donovan & Brian W. Kernighan.
// License: https://creativecommons.org/licenses/by-nc-sa/4.0/

package main

import (
	"fmt"
	"log"
	"net/http"
)

func main() {
	http.HandleFunc("/", handler) // each request calls handler
	log.Fatal(http.ListenAndServe("localhost:8000", nil))
}

// handler echoes the Path component of the requested URL.
func handler(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
}
```

This is the most basic form of HTTP server.

Type `go run filename.go` and the server is active, accepting incoming requests.

The `handler` function takes a ResponseWriter interface, which allows us to write back to the client, and the details of the HTTP request.

`http.Request` shows a lot of information on the incoming request:

```go
type Request struct {
        // Method specifies the HTTP method (GET, POST, PUT, etc.).
        // For client requests an empty string means GET.
        Method string

        // URL specifies either the URI being requested (for server
        // requests) or the URL to access (for client requests).
        //
        // For server requests the URL is parsed from the URI
        // supplied on the Request-Line as stored in RequestURI.  For
        // most requests, fields other than Path and RawQuery will be
        // empty. (See RFC 2616, Section 5.1.2)
        //
        // For client requests, the URL's Host specifies the server to
        // connect to, while the Request's Host field optionally
        // specifies the Host header value to send in the HTTP
        // request.
        URL *url.URL

        // The protocol version for incoming server requests.
        //
        // For client requests these fields are ignored. The HTTP
        // client code always uses either HTTP/1.1 or HTTP/2.
        // See the docs on Transport for details.
        Proto      string // "HTTP/1.0"
        ProtoMajor int    // 1
        ProtoMinor int    // 0

        // Header contains the request header fields either received
        // by the server or to be sent by the client.
        //
        // If a server received a request with header lines,
        //
        //	Host: example.com
        //	accept-encoding: gzip, deflate
        //	Accept-Language: en-us
        //	fOO: Bar
        //	foo: two
        //
        // then
        //
        //	Header = map[string][]string{
        //		"Accept-Encoding": {"gzip, deflate"},
        //		"Accept-Language": {"en-us"},
        //		"Foo": {"Bar", "two"},
        //	}
        //
        // For incoming requests, the Host header is promoted to the
        // Request.Host field and removed from the Header map.
        //
        // HTTP defines that header names are case-insensitive. The
        // request parser implements this by using CanonicalHeaderKey,
        // making the first character and any characters following a
        // hyphen uppercase and the rest lowercase.
        //
        // For client requests, certain headers such as Content-Length
        // and Connection are automatically written when needed and
        // values in Header may be ignored. See the documentation
        // for the Request.Write method.
        Header Header

        // Body is the request's body.
        //
        // For client requests a nil body means the request has no
        // body, such as a GET request. The HTTP Client's Transport
        // is responsible for calling the Close method.
        //
        // For server requests the Request Body is always non-nil
        // but will return EOF immediately when no body is present.
        // The Server will close the request body. The ServeHTTP
        // Handler does not need to.
        Body io.ReadCloser

        // GetBody defines an optional func to return a new copy of
        // Body. It is used for client requests when a redirect requires
        // reading the body more than once. Use of GetBody still
        // requires setting Body.
        //
        // For server requests it is unused.
        GetBody func() (io.ReadCloser, error)

        // ContentLength records the length of the associated content.
        // The value -1 indicates that the length is unknown.
        // Values >= 0 indicate that the given number of bytes may
        // be read from Body.
        // For client requests, a value of 0 with a non-nil Body is
        // also treated as unknown.
        ContentLength int64

        // TransferEncoding lists the transfer encodings from outermost to
        // innermost. An empty list denotes the "identity" encoding.
        // TransferEncoding can usually be ignored; chunked encoding is
        // automatically added and removed as necessary when sending and
        // receiving requests.
        TransferEncoding []string

        // Close indicates whether to close the connection after
        // replying to this request (for servers) or after sending this
        // request and reading its response (for clients).
        //
        // For server requests, the HTTP server handles this automatically
        // and this field is not needed by Handlers.
        //
        // For client requests, setting this field prevents re-use of
        // TCP connections between requests to the same hosts, as if
        // Transport.DisableKeepAlives were set.
        Close bool

        // For server requests Host specifies the host on which the
        // URL is sought. Per RFC 2616, this is either the value of
        // the "Host" header or the host name given in the URL itself.
        // It may be of the form "host:port". For international domain
        // names, Host may be in Punycode or Unicode form. Use
        // golang.org/x/net/idna to convert it to either format if
        // needed.
        //
        // For client requests Host optionally overrides the Host
        // header to send. If empty, the Request.Write method uses
        // the value of URL.Host. Host may contain an international
        // domain name.
        Host string

        // Form contains the parsed form data, including both the URL
        // field's query parameters and the POST or PUT form data.
        // This field is only available after ParseForm is called.
        // The HTTP client ignores Form and uses Body instead.
        Form url.Values

        // PostForm contains the parsed form data from POST, PATCH,
        // or PUT body parameters.
        //
        // This field is only available after ParseForm is called.
        // The HTTP client ignores PostForm and uses Body instead.
        PostForm url.Values

        // MultipartForm is the parsed multipart form, including file uploads.
        // This field is only available after ParseMultipartForm is called.
        // The HTTP client ignores MultipartForm and uses Body instead.
        MultipartForm *multipart.Form

        // Trailer specifies additional headers that are sent after the request
        // body.
        //
        // For server requests the Trailer map initially contains only the
        // trailer keys, with nil values. (The client declares which trailers it
        // will later send.)  While the handler is reading from Body, it must
        // not reference Trailer. After reading from Body returns EOF, Trailer
        // can be read again and will contain non-nil values, if they were sent
        // by the client.
        //
        // For client requests Trailer must be initialized to a map containing
        // the trailer keys to later send. The values may be nil or their final
        // values. The ContentLength must be 0 or -1, to send a chunked request.
        // After the HTTP request is sent the map values can be updated while
        // the request body is read. Once the body returns EOF, the caller must
        // not mutate Trailer.
        //
        // Few HTTP clients, servers, or proxies support HTTP trailers.
        Trailer Header

        // RemoteAddr allows HTTP servers and other software to record
        // the network address that sent the request, usually for
        // logging. This field is not filled in by ReadRequest and
        // has no defined format. The HTTP server in this package
        // sets RemoteAddr to an "IP:port" address before invoking a
        // handler.
        // This field is ignored by the HTTP client.
        RemoteAddr string

        // RequestURI is the unmodified Request-URI of the
        // Request-Line (RFC 2616, Section 5.1) as sent by the client
        // to a server. Usually the URL field should be used instead.
        // It is an error to set this field in an HTTP client request.
        RequestURI string

        // TLS allows HTTP servers and other software to record
        // information about the TLS connection on which the request
        // was received. This field is not filled in by ReadRequest.
        // The HTTP server in this package sets the field for
        // TLS-enabled connections before invoking a handler;
        // otherwise it leaves the field nil.
        // This field is ignored by the HTTP client.
        TLS *tls.ConnectionState

        // Cancel is an optional channel whose closure indicates that the client
        // request should be regarded as canceled. Not all implementations of
        // RoundTripper may support Cancel.
        //
        // For server requests, this field is not applicable.
        //
        // Deprecated: Use the Context and WithContext methods
        // instead. If a Request's Cancel field and context are both
        // set, it is undefined whether Cancel is respected.
        Cancel <-chan struct{}

        // Response is the redirect response which caused this request
        // to be created. This field is only populated during client
        // redirects.
        Response *Response
        // contains filtered or unexported fields
}
```

In this case, we're interested in `r.URL`, a URL struct defined in the net.url package:

```go
type URL struct {
        Scheme     string
        Opaque     string    // encoded opaque data
        User       *Userinfo // username and password information
        Host       string    // host or host:port
        Path       string
        RawPath    string // encoded path hint (Go 1.5 and later only; see EscapedPath method)
        ForceQuery bool   // append a query ('?') even if RawQuery is empty
        RawQuery   string // encoded query values, without '?'
        Fragment   string // fragment for references, without '#'
}
```

`r.URL.Path` prints the path currently requested, so - in short - the web server we just wrote at the moment is a simple echo of the request URL.

---

## Multiple request handlers

How can you setup a second request handler for a specific route, and let the original handler manage all the other route requests?

```go
package main

import (
	"fmt"
	"log"
	"sync"
)

func main() {
	http.HandleFunc("/", handler)
	http.HandleFunc("/about", aboutHandler)
	log.Fatal(http.ListenAndServe("localhost:8000", nil))
}

// handler echoes the Path component of the requested URL.
func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
}

// counter echoes the number of calls so far.
func aboutHandler(w http.ResponseWriter, r *http.Request) {
 	fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
    //...
}
```

Here all requests to _any_ URL are still handled by `handler()`, except `/count`. This is because passing the `pattern` parameter ending with `/` to `http.HandleFunc()` will cause a match of all subroutes, except a more specialized one is found.

## Accessing resources

The second web server example provides a way for handlers to manage common resources in a concurrency environment.

```go
// Copyright © 2016 Alan A. A. Donovan & Brian W. Kernighan.
// License: https://creativecommons.org/licenses/by-nc-sa/4.0/

package main

import (
	"fmt"
	"log"
	"net/http"
	"sync"
)

var mu sync.Mutex
var count int

func main() {
	http.HandleFunc("/", handler)
	http.HandleFunc("/count", counter)
	log.Fatal(http.ListenAndServe("localhost:8000", nil))
}

// handler echoes the Path component of the requested URL.
func handler(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	count++
	mu.Unlock()
	fmt.Fprintf(w, "URL.Path = %q\n", r.URL.Path)
}

// counter echoes the number of calls so far.
func counter(w http.ResponseWriter, r *http.Request) {
	mu.Lock()
	fmt.Fprintf(w, "Count %d\n", count)
	mu.Unlock()
}
```

This example uses a Mutex, because internally `http.HandleFun()` uses **goroutines** to fire the request handlers, and the `handler()` function increments a package variable. To avoid a **race condition** from happening, we must call Mutex.Lock before changing its value (same goes for `counter()` when printing its value).

## Printing the request headers

The book also presents a sample handler whose job is printing the request headers, well formatted:

```go
// Copyright © 2016 Alan A. A. Donovan & Brian W. Kernighan.
// License: https://creativecommons.org/licenses/by-nc-sa/4.0/

// handler echoes the HTTP request.
func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "%s %s %s\n", r.Method, r.URL, r.Proto)
	for k, v := range r.Header {
		fmt.Fprintf(w, "Header[%q] = %q\n", k, v)
	}
	fmt.Fprintf(w, "Host = %q\n", r.Host)
	fmt.Fprintf(w, "RemoteAddr = %q\n", r.RemoteAddr)
	if err := r.ParseForm(); err != nil {
		log.Print(err)
	}
	for k, v := range r.Form {
		fmt.Fprintf(w, "Form[%q] = %q\n", k, v)
	}
}
```

Opening the server in the browser will result in this output, for example:

```text
GET / HTTP/1.1
Header["Connection"] = ["keep-alive"]
Header["Accept"] = ["text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"]
Header["Accept-Language"] = ["en-us"]
Header["Accept-Encoding"] = ["gzip, deflate"]
Header["Upgrade-Insecure-Requests"] = ["1"]
Header["User-Agent"] = ["Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/603.1.30 (KHTML, like Gecko) Version/10.1 Safari/603.1.30"]
Header["Dnt"] = ["1"]
Host = "localhost:8000"
RemoteAddr = "127.0.0.1:51774"
```

