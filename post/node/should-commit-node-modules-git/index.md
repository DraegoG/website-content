---
title: Should you commit the node_modules folder to Git?
seotitle: Should I commit the node_modules folder to Git?
description: "That's a good question to have. There are pros and cons. I discuss the topic so you can make your own opinion."
date: 2018-08-06T07:00:00+02:00
tags: node
tags_weight: 15
path: should-commit-node-modules-git
---

Should you commit the node_modules folder to Git?

> I mention Git but the same applies to any version control system you happen to use

That's a good question to have. There are pros and cons.

I suggest the default is to _not_ commit the node_modules folder, and instead add it to your `.gitignore` file.

You might have special needs that reverse this decision.

I discuss the topic so you can make your own opinion.

## Here are some arguments in favor of not committing node_modules

You keep your Git history clean. When you add a new package, you store the [`package.json`](https://flaviocopes.com/package-json/) and [`package-lock.json`](https://flaviocopes.com/package-lock-json/) file changes.
When you decide to update the package version, all you store is the `package-lock.json` file change.

> `package-lock.json` is a relatively new feature of npm, that obsoletes the _shrinkwrap_ command used in the past

You avoid having to put possibly hundreds of MB of dependencies in your repository, and this means that over time it will be faster to work with. Switching branches and checking out the code are 2 operations hugely affected by the repository size.

When working with branches, you might have merge conflicts that extend beyond your code, and instead, involve dependencies code. This is not nice to deal with and might make you lose a lot of time. Avoiding putting

A pull request or merge if changing the dependencies, is going to have much more files involved in the process. Tools become slower or even decide to not show the full diff (GitHub, for example)

Native node modules need to be recompiled if you deploy to a platform different than your development machine(common use case: you develop on Mac, deploy on Linux). You need to call `npm rebuild`, which takes the server out of sync.

Not committing node_modules implies you need to list all your modules in the `package.json` (and `package-lock.json`) as a mandatory step. This is great because you might not have the diligence to do so, and some of the npm operations might break if you don't.

> Tip: there is no need to use the specific version in your `package.json` file, no more since the introduction of the `package-lock.json` file.

If you use separate `dependencies` and `devDependencies` sets, by committing the `node_modules` folder you're basically committing the `devDependencies` and there's no (easy) way for the production build to get rid of them.

## Reasons that might lead you to commit node_modules, and how to mitigate them

An [`npm`](https://flaviocopes.com/npm/) package might be removed by its author from the npm registry. It happened with the famous `left-pad` incident in 2016 ([read more](https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/)). This is very rare to happen for popular packages. If this happens, you might no longer have access to that particular piece of functionality.

You might also argue that `npm` is not guaranteed to stay around indefinitely, it might disappear, so an easy way to guarantee to have the full code of your application in the future is to commit it along with your app.

Every time you use a package, create a fork on GitHub. Every once in a while, keep it up to date with the origin (can be automated).

This is not always practical as packages can have dozens of their own dependencies.

You can use a private repository server for your project, and use that to host all your dependencies.

Options include

- [sinopia](https://github.com/rlidwka/sinopia)
- [npm_lazy](https://github.com/mixu/npm_lazy)
- [npm-lazy-mirror](https://www.npmjs.com/package/npm-lazy-mirror)
- [artifactory](https://jfrog.com/artifactory/)
- [npm Enterprise](https://www.npm-enterprise.com/), from the npm company

Another reason to commit the dependencies is the ability to quickly edit the code, if you find a bug or if you want to add something to a library.

This is a double-edged sword: if you do so, you lose the ability to upgrade the package if new releases are made, and it's just good for quick, temporary fixes.

The optimal solution is to either submit a PR that does what you want to the original project or fork it and use your fork as a dependency.