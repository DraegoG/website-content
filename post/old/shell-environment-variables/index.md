---
title: "How to set environment variables in bash and zsh"
date: 2017-08-27T11:04:59+02:00
updated: 2018-12-30T07:00:00+02:00
---

The operation is the same on both [**Bash**](/bash/) and **zsh**, with the caveat that to persist them you need to use `.bashrc` and `.zshrc`, respectively.

Setting them in the shell is the same:

```bash
$ export VARIABLE=something
```

To make sure it was set, type

```
$ $VARIABLE
```

If you edit a dot file, to apply the changes to the current shell use `source .dotfile`.

This works for Bash and Zsh.

With Fish you prepend `env`:

```fish
env API_KEY=123123 node app.js
```