---
title: Get the current folder in Node
seotitle: How to get the current folder in Node
description: "The two ways of referencing the filesystem: ./ and __dirname, explained"
date: 2018-08-09T15:00:00+02:00
tags: node
tags_weight: 27
path: node-get-current-folder
---

There are basically two ways to reference the current folder in a Node.js script:

- `./`
- `__dirname`

> Along with `./`, there is `../`, which points to the parent folder. They behave in the same way.

There is a big difference between the two.

Using `__dirname` in a Node script will return the path of the folder **where the current JavaScript file resides**.

Using `./` will give you the **current working directory**. It will return the same result as calling [`process.cwd()`](https://nodejs.org/api/process.html#process_process_cwd).

Initially the current working directory is the path of the folder where you ran the node command, but that can be changed during the execution of your script, by using the [`process.chdir()`](https://nodejs.org/api/process.html#process_process_chdir_directory) API.

There is just one place where `./` refers to the current file path, and it's in a `require()` call. In there, `./` (for convenience) will always refer to the JavaScript file path, letting you import other modules based on the folder structure.
