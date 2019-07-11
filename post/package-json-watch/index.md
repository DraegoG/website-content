---
title: "Run package.json scripts upon any file changes in a folder"
date: 2018-07-01T07:06:15+02:00
description: "This article explains how to make a package.json script re-run whenever a file in a folder changes."
---

My practical problem: I want to automatically regenerate the CSS, going through a PostCSS pipeline, upon file changes.

The approach I describe will work for any kind of automatic file and folder watching, not just for this specific case.

I have this script in action, which I run using `yarn build:css`:

```json
"scripts": {
  "build:css": "postcss src/tailwind.css -o static/dist/tailwind.css",
}
```

and I want to re-run it whenever something changes in the `layouts` folder, which contains all the HTML files that build up my site.

If you're familiar with Tailwind, it creates a slightly big CSS files with all the things you might need, and you can optimize it by removing any class you don't use.

Every time I change something in there, I want to regenerate the CSS, and trigger the purge and minification I set up in the [PostCSS](/postcss/) setup.

How to do this?

Install the [`watch`](https://www.npmjs.com/package/watch) npm package:

```bash
npm install watch
```

and add the `watch` script to your `package.json` file. You already had `build:css` from before, we just add a script that watches the layouts folder and runs `build:css` upon every change:

```json
"scripts": {
  "build:css": "postcss src/tailwind.css -o static/dist/tailwind.css",
  "watch": "watch 'npm run build:css' ./layouts"
}
```

Now run `npm run watch` or `yarn watch`.
