---
title: "Configuring the macOS command line"
description: "How to set up the macOS terminal from zero to a perfect tool for you day to day development"
date: 2019-02-10T07:00:00+02:00
tags: devtools
---

> See my [how to use the macOS terminal](/macos-terminal/) post too

# How to setup the macOS command line
I just got a new MacBook Air to replace my beloved 2010 MacBook Pro, and I decided to document the process of setting up the command line.

By default here's what we have:

![](Screenshot 2019-01-29 at 18.34.04.png)

We're going to have a much better terminal at the end of this article.

First thing is, install *Homebrew*. Head to https://brew.sh and copy the magic formula in your terminal, which should be:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

This will take care of installing the Brew package manager, which is an incredible tool. It will take some time as it needs to download the Xcode command line tools from Apple.

![](Screenshot 2019-01-30 at 07.41.04.png)

Next thing, we install the [*Fish Shell*](/fish-shell/). Run `brew install fish`.

Now we need to make Fish our default shell. Run `sudo vim /etc/shells`, and press the `i` key to enter *insert mode*, then add `/usr/local/bin/fish` at the end of this list.

![](Screenshot 2019-01-30 at 07.46.31.png)

Now press the `esc` key and then type `:wq` to save the file and exit the editor.

Type `chsh -s /usr/local/bin/fish` to change your default shell to Fish.

Try opening a new terminal window, you'll see Fish greeting you:

![](Screenshot 2019-01-30 at 07.48.13.png)

Time to add some colour. Type `fish_config` to enter the (awesome) configuration tool:

![](Screenshot 2019-01-30 at 07.49.11.png)

Pick one theme and press "Set Theme". Then click the  `prompt`  to set the favourite prompt and click "Set Prompt". My favourite is Rubbyrussell:

![](Screenshot 2019-01-30 at 07.51.52.png)

Now exit and press `enter` in the shell, to close the configuration program.

Your shell should now have a nice prompt, and colours! We just need to change the background - that needs to be set in the Terminal app preferences.

![](Screenshot 2019-01-30 at 07.53.34.png)

Press `cmd-,` or click `Terminal -> Preferences`.

Go to this GitHub repository: https://github.com/lysyi3m/macos-terminal-themes.

![](Screenshot 2019-01-30 at 08.00.10.png)

There is a huge number of great themes to choose from. One I like is Dracula (https://github.com/lysyi3m/macos-terminal-themes/blob/master/schemes/Dracula.terminal)  Just click the "Raw" button and save it as `Dracula.terminal`.

Right-click it and click "Open", as it's not a signed binary (otherwise macOS prevents it from running). That's it! The theme is now applied and available in the configuration:

![](Screenshot 2019-01-30 at 08.01.19.png)

![](Screenshot 2019-01-30 at 07.59.39.png)

Next thing, the font. I like to use Fira Code, a free programmers friendly font with ligatures (the nice things with arrows).  Download it from https://github.com/tonsky/FiraCode, open its `ttf` folder, select all files, right-click and press `Open` to install it.

![](Screenshot 2019-01-30 at 08.12.21.png)

Go back to the terminal configuration, and set it as your theme font. Open a new window, and it should be working fine:

![](Screenshot 2019-01-30 at 08.13.24.png)

That's it!
