---
title: "How to discover a bug using git bisect"
date: 2019-01-09T07:00:00+02:00
description: "How I debug almost all problems that involve a long history of changes, tracked using Git, and discover when you introduced a bug in your code"
tags: git
---

Sometimes we work on projects for a long, long time. We might craft the perfect 1.0 release, then we release it to the public and we start working on bug fixes, then we get feature requests and we work on improving the app.

At some point during this process you get a **regression bug**: an unexpected problem that is caused by an unrelated change in the code.

Something is not working as expected, although you didn't really change that part of code recently.

Or maybe you touched a file or function so many times that you can't remember what change might have caused the problem that was reported to you.

In any case, the first thing to do is to **determine where the bug is**.

If you work using a versioning control system like [Git](/git/), things are easier. You can go back in time and figure out the exact commit that introduced the change. When working in teams this is important because some other person might have worked on that, and if they caused the error you might not know what to do - except asking them to fix it, because Git gives you this information.

One way to do this is to manually checkout some specific commit. For example you can start by checking if yesterday's version of the codebase worked fine.

I use [GitHub Desktop](https://desktop.github.com), the awesome Git client by [GitHub](/github/). It's great for day to day use, but it does not let me check out a single commit. Some other clients do, but you can use the [command line](/macos-terminal/).

Run

```bash
git checkout <COMMIT_SHA>
```

where <COMMIT_SHA> is the commit you want to roll back to. It will look something like `5a06d3ca5e7adb6e67`.

If you still got the problem, you try doing the same with another commit from the day before, and so on, until you find a commit where the code works.

Now you need to apply the **divide and conquer** principle, and pick a commit in the middle of the last one that you tried (and didn't work) and the one that works.

Repeat the process and cut in half every time the interval of commits, until you identify the commit that introduced the problem.

This is such a common and useful thing that Git introduced the `bisect` command to automate this process.

Start from your latest commit. Use `git checkout your-branch-name`, for example `git checkout master` if you already checked out an older commit.

Then run:

```bash
git bisect start
```

Nothing happened yet. You need to tell Git a *bad* commit reference, where the code does not work:

```bash
git bisect bad HEAD
```

and a *good* commit, where the code worked:

```bash
git bisect good 7f4d976e7540e28c6b0
```

Git starts the process:

```bash
Bisecting: 3 revisions left to test after this (roughly 2 steps)
[d18ebf1c7db9a9b44e8facc5ddb3551e641a64e2] fixes #25
```

See, you have 6 commits between HEAD and the commit I mentioned as good. Git tells me I have 2 more steps until we find the problematic commit.

I go and test the code, then I tell Git the result: `git bisect bad` or `git bisect good` depending on the success.

Repeat until you find the bad commit, and then run `git bisect reset` to get back to the HEAD commit.

Git will guide you in this operation of bisecting. You enter the SHA of the commit