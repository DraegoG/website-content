---
title: "Async vs sync code"
description: "The difference between running code synchronously or asynchronously"
tags: js
date: 2018-10-16T07:00:00+02:00
---

You might have heard that Node.js is fast because it provide asynchronous APIs for all expensive operations, like network access or filesystem.

What does having an asynchronous API mean?

If you anticipate an operation can take a lot of time, it makes sense to run it asynchronously, so other code can run in the meantime, and have a hook that's called when that operation ends.

This is how Node.js can handle a lot more traffic than, say, PHP or Rails without using async libraries.

Most programming languages that were not traditionally async today do have 3rd party libraries that implement ways to call asynchronous code.

Otherwise what usually happens for example in PHP or Python code is that the thread blocks until the sync operation (reading from the network, writing a file..) ends.

If the code runs asynchronously, the CPU is not idle waiting for the process to complete, but it can go on with other tasks queued up until the original process is ready to move on.