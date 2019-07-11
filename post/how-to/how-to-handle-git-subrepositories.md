---
title: An easy way to handle Git subrepositories
description: "In this post I describe the simplest way I found to manage Git subrepositores."
date: 2015-05-14T09:06:59+02:00
tags: git
---

> Warning: this post is old and might not reflect the current state of the art

Suppose in your project you have a folder that you want to manage on a separate Git repository.

Or, suppose you want to open-source part of your application, but you don't want the burden of managing a separate folder, symlinks and separate Git pushes.

What can you do?

## Enter subtrees

First, create a new repository that will host the files you need. If using GitHub, initialize it with a README.md file so it will automatically create the `master` branch.

Next, add it as a remote inside your project.

    $ git remote add repository-name git@github.com:yourname/repository-name.git
    $ git subtree add --prefix=subfolder/path/you/want repository-name master

Change `repository-name`, `subfolder/path/you/want` and `yourname` with your chosen names.

You can add `--squash` to the last command if the project want to incorporate has already many commits, and you want to pull all changes in one single commit.

You're done!

## Pushing and pulling

Now, suppose someone pushes a PR on that subrepository, or you edit it from another project.

To incorporate the changes inside your project, do:

    git subtree pull --prefix=subfolder/path/you/want repository-name master

You can add `--squash` if you want to incorporate all changes in one single commit.

Now you'll push to your own project, and the changes made in the subrepository are stored in the Git history of it.

To *also* push those changes to the subrepository Git history, and to the remote, just do

    git subtree push --prefix=subfolder/path/you/want repository-name master

Again, use `--squash` if you feel it appropriate. Git will cherry-pick the commits that involve the subrepository subdirectory, so you'll just see those changes in the subrepository history.

You might want to be careful and differentiate the commits that involve the subrepository. In this way you'll keep things separated.
