---
title: "How to hide the address bar in Chrome"
date: 2018-11-16T07:00:00+02:00
description: "Useful for screenshots and screencasts, or just to increase the real estate of your screen"
---

There is no easy way from within an open instance of Chrome. You need to go to the terminal and open a new Chrome instance in *application mode*, passing the URL.

## OSX

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --app=URL
```

## Windows

```bash
Chrome.exe --app=URL
```

(prepent Chrome.exe with the Chrome folder, which varies by Windows version - [see here](https://stackoverflow.com/questions/40674914/google-chrome-path-in-windows-10/40674915))

## Linux

```bash
google-chrome --app=URL
```