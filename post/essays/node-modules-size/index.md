---
title: The node_modules folder size is not a problem. It's a privilege
date: 2019-01-30T07:00:00+02:00
description: "My thoughts on the node_modules folder size debate"
tags: js
---

I used to get mad at the `node_modules` folder size. How can a JavaScript application be 100, 200MB in size without even me adding any line of code? I just run `npx create-react-app todolist` and I downloaded 218,7MB of _stuff_! (I just checked it now, that's a real number).

Whenever you think about the size of node_modules, think about the millions of man hours that we programmers put into it.

This is all Open Source software. Software you can inspect and learn from. Kindly donated by programmers and companies all over the world.
It's a global effort that someone made very simple to benefit from. It happened to be `npm`, the tool first, and the company next.

We all agreed to publish our code to their servers, and people built things on top, other things on top, until we got to the point that we had quick starters (like create-react-app or the Vue CLI for example) that we can use to get lots of power into our hands for free.

Is 200MB too much in the era of TB-order fast storage?

Keep in mind that the vast majority of this size is tests, documentation, and what not. And also the vast majority of the code remaining is only used in the development environment. It's not like you will serve a 200MB application to the client, I think this is well understood.

I took the example of create-react-app. What's in those 200MB?

To start with, create-react-app contains

- a compiler (Babel)
- a bundler (Webpack)
- a code minifier
- a linter (ESLint)
- a styling pipeline tool (SCSS)
- a development server with live reloading
- a test runner (Jest)

If you want to write a Mac or iPhone application, you have to install `Xcode`, the IDE provided by Apple. `Xcode` is (wait for it..) almost 14GB in size. That's 70x the size of node_modules. Granted, we're comparing two different things, but node_modules contains all you need to start working on your code. You can pair it with VS Code which is 200MB in size, or with Sublime Text which is 30MB - does not matter, no one is even strictly required (while you can't create an iOS/macOS app without `Xcode`).

If the concern is your hard disk filling
up with modules, [`pnpm`](https://pnpm.js.org/) is an optimal drop-in solution which centralizes modules in one location and all your apps use those modules instead of making their own local version. It's used by online coding tools like [Glitch](/glitch/) for example.

I've read people wonder how they can audit the codebase for security issues or other problems if our apps rely on too much code written by others.

It's a choice, right? You are not forced to use modules. You can create your own version of tooling that does not require all those modules, but then you'll have to maintain that code, test it, manage new releases when things need to be updated, and more _work_.

I've had the opportunity to work with other languages and ecosystem where the vibrancy and opportunities of npm would have been a blessing, and instead I had to build my own little library for everything, as the things I found distributed by 3rd part developers were either non-existent or abandoned since a couple years, and not kept up to date with the rest of the language.

Maybe we could have a flag to only download production code rather than all documentation, tests, and what not? But this is just an idea that came to mind now, not sure how this would be doable.

Anyway: long live, `node_modules`!