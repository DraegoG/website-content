---
title: UNIX Editors
date: 2019-02-18T15:00:00+02:00
description: "A brief guide to the UNIX editors"
tags: cli
---

Any UNIX system provides many different editors out of the box. In this section I will describe the most popular ones showing the basics of working with them. `vim` and `emacs` in particular have lots and lots of different commands, have plugins, and so you can spend years using them just scratching the surface of what's possible.

## `ed`

`ed` is the original UNIX text editor, and it's the most basic you can work with. It's also very rarely used, if _ever_ used, by most people.

Run it by typing `ed`. This starts an interactive session. Enter in write mode by typing `a` on a single line, and press `enter`. Then type everything you want, and once you are done, write just a dot (`.`) on a line and press `enter`.

Now type `w` followed by a file name to save the buffer to a file. It will return the number of bytes written to the file.

You can then press `q` to quit.

You can edit a file with `ed` by invoking it with the file name: `ed <filename>`. When you press `a` to add, you add content to the bottom of the file.

Inside an `ed` session you can type `,p` to print the current file content.

## `vi` / `vim`

`vim` is a **very** popular file editor, especially among programmers. It's actively developed and frequently updated, and there's a very big community around it. There's even a [Vim conference](https://vimconf.org/)!

`vi` in modern systems is just an alias to `vim`, which means `vi` i`m`proved.

You start it by running `vi` on the command line.

![](Screenshot%202019-02-10%20at%2011.44.36.png)

You can specify a filename at invocation time to edit that specific file:

```bash
vi test.txt
```
![](Screenshot%202019-02-10%20at%2011.36.21.png)

You have to know that Vim has 2 main modes:

- *command* (or *normal*) mode
- *insert* mode

When you start the editor, you are in command mode. You can't enter text like you expect from a GUI-based editor. You have to enter **insert mode**. You can do this by pressing the `i` key. Once you do so, the `-- INSERT --` word appear at the bottom of the editor:

![](Screenshot%202019-02-10%20at%2011.47.39.png)

Now you can start typing and filling the screen with the file contents:

![](Screenshot%202019-02-10%20at%2011.48.39.png)

You can move around the file with the arrow keys, or using the `h` - `j` - `k` - `l` keys. `h-l` for left-right, `j-k` for down-up.

Once you are done editing you can press the `esc` key to exit insert mode, and go back to **command mode**.

![](Screenshot%202019-02-10%20at%2011.48.44.png)

At this point you can navigate the file, but you can't add content to it (and be careful which keys you press as they might be commands).

One thing you might want to do now is **saving the file**. You can do so by pressing `:` (colon), then `w`.

You can **save and quit** pressing `:` then `w` and `q`: `:wq`

You can **quit without saving**, pressing `:` then `q` and `!`: `:q!`

You can **undo** and edit by going to command mode and pressing `u`. You can **redo** (cancel an undo) by pressing `ctrl-r`.

Those are the basics of working with Vim. From here starts a rabbit hole we can't go into in this little introduction.

I will only mention those commands that will get you started editing with Vim:

- pressing the `x` key deletes the character currently highlighted
- pressing `A` goes at the end of the currently selected line
- press `0` to go to the start of the line
- go to the first character of a word and press `d` followed by `w` to delete that word. If you follow it with `e` instead of `w`, the white space before the next word is preserved
- use a number between `d` and `w` to delete more than 1 word, for example use `d3w` to delete 3 words forward
- press `d` followed by `d` to delete a whole entire line. Press `d` followed by `$` to delete the entire line from where the cursor is, until the end

To find out more about Vim I can recommend the [Vim FAQ](https://vimhelp.org/vim_faq.txt.html) and especially running the `vimtutor` command, which should already be installed in your system and will greatly help you start your `vim` explorations.

## `emacs`

`emacs` is an awesome editor and it's historically regarded as _the_ editor for UNIX systems. Famously `vi` vs `emacs` flame wars and heated discussions caused many unproductive hours for developers around the world.

`emacs` is  very powerful. Some people use it all day long as a kind of operating system (https://news.ycombinator.com/item?id=19127258). We'll just talk about the basics here.

You can open a new emacs session simply by invoking `emacs`:

![](Screenshot%202019-02-10%20at%2012.14.18.png)

> macOS users, stop a second now. If you are on Linux there are no problems, but macOS does not ship applications using GPLv3, and every built-in UNIX command that has been updated to GPLv3 has not been updated. While there is a little problem with the commands I listed up to now, in this case using an emacs version from 2007 is not exactly the same as using a version with 12 years of improvements and change. This is not a problem with Vim, which is up to date. To fix this, run `brew install emacs` and running `emacs` will use the new version from Homebrew (make sure you have [Homebrew](https://brew.sh) installed)

You can also edit an existing file calling `emacs <filename>`:

![](Screenshot%202019-02-10%20at%2013.12.49.png)

You can start editing and once you are done, press `ctrl-x` followed by `ctrl-w`. You confirm the folder:

![](Screenshot%202019-02-10%20at%2013.14.29.png)

and Emacs tell you the file exists, asking you if it should overwrite it:

![](Screenshot%202019-02-10%20at%2013.14.32.png)

Answer `y`, and you get a confirmation of success:

![](Screenshot%202019-02-10%20at%2013.14.35.png)

You can exit Emacs pressing `ctrl-x` followed by `ctrl-c`.
Or `ctrl-x` followed by `c` (keep `ctrl` pressed).

There is a lot to know about Emacs. More than I am able to write in this little introduction. I encourage you to open Emacs and press `ctrl-h` `r` to open the built-in manual and `ctrl-h` `t` to open the official tutorial.

## `nano`

`nano` is a more beginner friendly editor.

Run it using `nano <filename>`.

You can directly type characters into the file without worrying about modes.

You can quit without editing using `ctrl-X`. If you edited the file buffer, the editor will ask you for confirmation and you can save the edits, or discard them. The help at the bottom shows you the keyboard commands that let you work with the file:

![](Screenshot%202019-02-10%20at%2011.03.51.png)

`pico` is more or less the same, although `nano` is the GNU version of `pico` which at some point in history was not open source and the `nano` clone was made to satisfy the GNU operating system license requirements.