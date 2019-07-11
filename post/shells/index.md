---
title: "Unix Shells Tutorial"
date: 2019-08-20T07:00:00+02:00
description: "An introduction to Unix shells and how to use them"
tags: cli
---

A shell is a command interpreter that exposes an interface to the underlying operating system.

It allows you to execute operations using text and commands, and it provides users advanced features like being able to create scripts.

This is important: shells let you perform things in a more optimized way than a GUI (Graphical User Interface) could ever possibly let you do. Command line tools can offer many different configuration options without being too complex to use.

There are many different kind of shells. This post focuses on Unix shells, the ones that you will find commonly on Linux and macOS computers.

Many different kind of shells were created for those systems over time, and a few of them dominate the space: Bash, Csh, Zsh, Fish and many more!

All shells originate from the Bourne Shell, called `sh`. "Bourne" because its creator was Steve Bourne.

Bash means *Bourne-again shell*. `sh` was proprietary and not open source, and Bash was created in 1989 to create a free alternative for the GNU project and the Free Software Foundation. Since projects had to pay to use the Bourne shell, Bash became very popular.

In this post I will describe things that we can consider common in all modern shells, and if there's something shell-specific, I will add a note.

## Starting a shell

Try opening your [Mac terminal](/macos-terminal/). That by default is running Bash, the most common shell. You can set up your system to run any kind of shell, for example I use Fish.

But let's start from the defaults and assume you use Bash.

What you will see now is a prompt, most probably `$`. You can type anything, and upon pressing the `enter` key, the shell will interpret your command and try to execute the line you entered.

## Learn more

I just made a simple introduction to the basics. Each single shell has its own unique features and advanced usage.

Check those posts about each specific shell for more on their usage:

- [Bash](/bash/)
- [Fish](/fish-shell/)
