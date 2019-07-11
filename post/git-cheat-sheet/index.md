---
title: A Git Cheat Sheet
description: This page contains a list of Git commands I find handy to know but I find hard to remember
date: 2014-01-11T09:06:29+02:00
tags: git
---

<!-- TOC -->

- [Squash a series of commits and rewrite the history by writing them as one](#squash-a-series-of-commits-and-rewrite-the-history-by-writing-them-as-one)
- [Take a commit that lives in a separate branch and apply the same changes on the current branch](#take-a-commit-that-lives-in-a-separate-branch-and-apply-the-same-changes-on-the-current-branch)
- [Restore the status of a file to the last commit (revert changes)](#restore-the-status-of-a-file-to-the-last-commit-revert-changes)
- [Show a pretty graph of the commit history](#show-a-pretty-graph-of-the-commit-history)
- [Get a prettier log](#get-a-prettier-log)
- [Get a shorter status](#get-a-shorter-status)
- [Checkout a pull request locally](#checkout-a-pull-request-locally)
- [List the commits that involve a specific file](#list-the-commits-that-involve-a-specific-file)
- [List the commits that involve a specific file, including the commits content](#list-the-commits-that-involve-a-specific-file-including-the-commits-content)
- [List the repository contributors ordering by the number of commits](#list-the-repository-contributors-ordering-by-the-number-of-commits)
- [Undo the last commit you pushed to the remote](#undo-the-last-commit-you-pushed-to-the-remote)
- [Pick every change you haven't already committed and create a new branch](#pick-every-change-you-havent-already-committed-and-create-a-new-branch)
- [Stop tracking a file, but keep it in the file system](#stop-tracking-a-file-but-keep-it-in-the-file-system)
- [Get the name of the branch where a specific commit was made](#get-the-name-of-the-branch-where-a-specific-commit-was-made)

<!-- /TOC -->

### Squash a series of commits and rewrite the history by writing them as one

`git rebase -i`

this puts you in the interactive rebasing tool.

Type `s` to apply `squash` to a commit with the previous one. Repeat the `s` command for as many commits as you need.

### Take a commit that lives in a separate branch and apply the same changes on the current branch

single commit:

`git cherry-pick <commit>`

for multiple commits:

`git cherry-pick <commit1> <commit2> <commit3>`

### Restore the status of a file to the last commit (revert changes)

`git checkout -- <filename>`

### Show a pretty graph of the commit history

`git log --pretty=format:"%h %s" --graph`

### Get a prettier log

`git log --pretty=format:"%h - %an, %ar : %s"`

### Get a shorter status

`git status -s`

### Checkout a pull request locally

`git fetch origin pull/<id>/head:<branch>`

`git checkout <branch>`

### List the commits that involve a specific file

`git log --follow -- <filename>`

### List the commits that involve a specific file, including the commits content

`git log --follow -p -- <filename>`

### List the repository contributors ordering by the number of commits

`git shortlog -s -n`

### Undo the last commit you pushed to the remote

`git revert -n HEAD`

### Pick every change you haven't already committed and create a new branch

`git checkout -b <branch>`

### Stop tracking a file, but keep it in the file system

`git rm -r --cached`

### Get the name of the branch where a specific commit was made

`git branch --contains <commit>`