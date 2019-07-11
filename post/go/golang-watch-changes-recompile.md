---
title: "Go, how to watch changes and rebuild your program"
date: 2017-08-26T15:46:52+02:00
tags: go
---

Today I found this nice tool: <https://github.com/canthefason/go-watcher>

You can run it inside a folder that contains your Go files, by executing `watcher`.

It builds the application, and when you change any of the files it recompiles it again. Very handy especially for API services that need to be restarted every time you change something.

There are many options you can customize, including running it inside a Docker container.

Happy coding!