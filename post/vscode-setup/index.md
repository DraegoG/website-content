---
title: "Configuring VS Code"
description: "How to set up VS Code from zero to a perfect tool for JavaScript development"
date: 2019-02-09T07:00:00+02:00
tags: devtools
---

I recently got a new Mac (a MacBook Air) and I had to install a fresh VS Code, so I took the time to document what I did to make my coding experience equivalent to my old MacBook Pro, which lasted the enormous amount of 9 years.

> See my [VS Code introduction](/vscode/) post too

Here is what I did:

1. I installed [Fira Code](https://github.com/tonsky/FiraCode) and set it as my Font Family
2. I set Tab Size to 2 (this is my religion). Spaces. 2 spaces.
3. I added `**/node_modules` to the Excluded Files to prevent them to show up in the file list
4. I enabled *Format on Paste* and *Format on Save*
5. Enabled **font ligatures**
6. Disabled the Minimap
7. Enabled *Trim Trailing Whitespace*
8. I installed the [Sublime Text Keymap plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings). It gives the `cmd-K cmd-B` shortcut to show/hide the sidebar, `cmd-W` to close a file and more.

Next I installed some themes. It depends on your taste. I like to switch between

- Palenight Theme
- Nostromo
- Night Owl
- Ayu

Next I installed these extensions:

- Prettier
- IntelliSense for CSS class names
- Intent 4-to-2
- ESLint
- Duplicate action
- Bracket Pair Colorizer 2
- Babel ES6/ES7
- ES7 React/Redux/GraphQL/React-Native snippets
- TODO Highlight

This is a good set to start working with JavaScript and React.

This is my user settings JSON after configuring all according to my taste and needs:

```json
{
    "editor.fontFamily": "Fira Code",
    "editor.tabSize": 2,
    "editor.wordWrap": "bounded",
    "files.exclude": {
        "**/node_modules": true
    },
    "editor.formatOnPaste": true,
    "editor.formatOnSave": true,
    "editor.minimap.enabled": false,
    "workbench.colorTheme": "Tomorrow Night Blue",
    "files.trimTrailingWhitespace": true,
    "workbench.activityBar.visible": false,
    "window.zoomLevel": 2,
    "editor.cursorBlinking": "smooth",
    "editor.fontLigatures": true,
    "prettier.jsxBracketSameLine": true,
    "prettier.jsxSingleQuote": true,
    "prettier.singleQuote": true,
    "prettier.semi": false,
    "[markdown]": {
        "editor.renderWhitespace": "all",
        "editor.acceptSuggestionOnEnter": "off",
        "editor.parameterHints.enabled": false,
        "editor.quickSuggestions": false,
        "editor.snippetSuggestions": "none",
    }
}
```

The `[markdown]` section adds Markdown-specific configuration. In this case I disable all the popups that distract me while writing, which are otherwise useful when coding.

That's it.

Also check out [VS Code setup for React development](/vscode-react-setup/)!

Happy coding!