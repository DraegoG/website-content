---
title: How to fix the "Missing write access" error when using npm
description: "Quickly solve this annoying problem when installing global packages using npm"
date: 2019-04-18T15:00:00+02:00
tags: node
---

The first time you try to install a package globally using [npm](/npm/), using the syntax `npm install -g <package>` on a Mac, or Linux, you might get a weird error, saying something like

```txt
Missing write access to /usr/local/lib/node_modules
```

![npm error message](error-npm-permission.png)

or something along those lines, followed by a long list of other errors of warnings, a consequence of the first error that's printed to you.

This error is preventing us to install the package.

How do you fix this? It's a permission error, which means you don't have write access to that folder.

This is how to solve it. Run this command:

```sh
sudo chown -R $USER /usr/local/lib/node_modules
```

Let's break it down:

`sudo` means we are running this command as `root`, the system super user. This is because we don't have permission to write to that folder, but `root` will be able to fix any permission. This command also means the system will ask for your password to confirm.

`chown` is the command we use to change the owner of a file or folder. We set the `-R` option to change the owner recursively, so we also get owner access to all the files already contained in there.

`$USER` is an environment variable automatically set to your username.

And the final piece is the folder path.

Running this path will make the folder *yours*, so you can safely run your `npm install -g <package>` commands!

Pay attention to the folder listed by the error message. If it's different, update the `chown` command accordingly.