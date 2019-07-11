---
title: "Using NGINX Reverse Proxy to serve Go services"
date: 2016-02-28T13:30:17+02:00
tags: go
---

One of the most common ways to expose a Go application to the world is through a reverse proxy.

NGINX makes this very easy. This NGINX configuration serves 2 different applications listening on port 8001 and 8002 respectively.

```sh
server {
   listen 80 default_server;
   server_name your-domain;

   location /go-service-1 {
      proxy_set_header X-Real-IP $remote_addr;
      proxy_pass http://localhost:8001;
   }

   location /go-service-2 {
      proxy_set_header X-Real-IP $remote_addr;
      proxy_pass http://localhost:8002;
   }
}
```

Using `proxy_set_header X-Real-IP $remote_addr` ensures that you'll have the visitor's real address in `http.Request.Header.Get("X-Real-IP")`

The 8081 and 8082 ports can now stay private, and NGINX serves them from a single point of entry.