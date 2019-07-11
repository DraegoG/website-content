---
title: What is pnpm?
date: 2019-02-02T07:00:00+02:00
description: "Introduction to pnpm, the drop in npm replacement that saves you disk space"
tags: node
---

I recently wrote about how we have huge `node_modules` folders and why this is not necessarily a bad thing, but it would be reduce that hard drive consumption, right?

Every byte saved on disk can be used for something else than libraries code, I have a 512GB SSD on my MacBook Pro I bought in 2010 but some brand new computers in 2019 ship with a 128GB SSD (something went wrong with Moore's Law when it comes to hard disk space).

In particular, one way would be to centralize the libraries code storage into a central place, and share it with all the projects you work on.

This is the main value proposition of *pnpm*, a very cool project you can check out at <https://pnpm.js.org>.

It is basically a drop-in replacement for [`npm`](/npm/), which means that once you install it, you can invoke `pnpm install` to download a project dependencies, and all will work transparently for you.

If you have 10 projects that use React, at the same version, `pnpm` will install it once, and then reference that first install across all your other projects.

This also means that the project initialization part takes much less time than if it had to download resources using the standard `npm` procedure. It's faster even if `npm` cached the package, because `pnpm` makes a hard link to the central local repository, while `npm` makes a copy of the package from the cache.

You install `pnpm` using `npm`, of course 😁

```bash
npm install -g pnpm
```

Then being `pnpm` a drop-in replacement, you can use all the `npm` commands:

```bash
pnpm install react
pnpm update react
pnpm uninstall react
```

and so on.

`pnpm` is especially appreciated in those companies where there is a need to maintain a large number of projects with the same dependencies.

For example [Glitch](/glitch/) is one of those companies, as they host a gazillion Node.js projects.

`pnpm` gives them, in addition to the `npm` usual commands, some utilities including [`pnpm recursive`](https://pnpm.js.org/docs/en/pnpm-recursive.html), which is used to run the same command across all the projects in a folder. For example you can initialize 100 projects stored in the current folder by running `pnpm recursive install`. Handy.

If you use [`npx`](/npx/), which is a handy (and the recommended) way to run utilities like `create-react-app`, you'll get the benefits of `pnpm` by using the `pnpx` command which comes with `pnpm`:

```bash
pnpx create-react-app my-cool-new-app
```

Where are the packages installed? In macOS, in the `~/.pnpm-store/` folder (where `~` means your home folder). I installed `lodash` as an example and this was the resulting folder structure:

```bash
➜  ~ tree .pnpm-store/
.pnpm-store/
└── 2
    ├── _locks
    ├── registry.npmjs.org
    │   └── lodash
    │       ├── 4.17.11
    │       │   ├── integrity.json
    │       │   ├── node_modules
    │       │   │   └── lodash
    │       │   │       ├── ...
    │       │   ├── package -> node_modules/lodash
    │       │   └── packed.tgz
    │       └── index.json
    └── store.json
```

There are many more advanced things to learn about the tool, but I hope this helps getting you started with `pnpm`!

Should you use it for a day-to-day use? Probably not, just stick to `npm` unless you have needs that this tool solves for you - lack of disk space being one of them.