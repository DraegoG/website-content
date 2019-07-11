---
title: Where does npm install the packages?
description: "How to find out where npm installs the packages"
date: 2018-08-03T15:00:00+02:00
tags: node
tags_weight: 12
path: where-npm-install-packages
---

> Read the [npm guide](https://flaviocopes.com/npm/) if you are starting out with npm, it's going to go in a lot of the basic details of it.

When you install a package using `npm` (or [yarn](https://flaviocopes.com/yarn/)), you can perform 2 types of installation:

- a local install
- a global install

By default, when you type an `npm install` command, like:

```bash
npm install lodash
```

the package is installed in the current file tree, under the `node_modules` subfolder.

As this happens, `npm` also adds the `lodash` entry in the `dependencies` property of the [`package.json` file](https://flaviocopes.com/package-json/) present in the current folder.

A global installation is performed using the `-g` flag:

```bash
npm install -g lodash
```

When this happens, npm won't install the package under the local folder, but instead, it will use a global location.

Where, exactly?

The `npm root -g` command will tell you where that exact location is on your machine.

On macOS or Linux this location could be `/usr/local/lib/node_modules`.
On Windows it could be `C:\Users\YOU\AppData\Roaming\npm\node_modules`

If you use `nvm` to manage Node.js versions, however, that location would differ.

I for example use `nvm` and my packages location was shown as   `/Users/flavio/.nvm/versions/node/v8.9.0/lib/node_modules`.
