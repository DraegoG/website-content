---
title: "VS Code: use language-specific settings"
date: 2017-08-19T11:04:59+02:00
updated: 2018-05-28T11:04:59+02:00
tags: devtools
---

With VS Code you have the ability to customize your spaces vs tabs preference, like in any editor, and also the option to choose how many spaces should a tab take.

Different languages however might require different settings.

For example I like to have 4 spaces in HTML, but only 2 in CSS and JavaScript.

Go on the other hand wants 8 spaces.

How to deal with this?

You can add language-specific settings into the VS Code preferences file (opened with `cmd+,`).

This is an example that uses different settings for JS, CSS, HTML and Go files:

```js
"[javascript]": {
    "editor.insertSpaces": true,
    "editor.tabSize": 2
},
"[css]": {
    "editor.insertSpaces": true,
    "editor.tabSize": 2
},
"[html]": {
    "editor.insertSpaces": true,
    "editor.tabSize": 4
},
"[go]": {
    "editor.insertSpaces": false,
    "editor.tabSize": 8
}
```