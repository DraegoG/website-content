---
title: "VS Code setup for React development"
description: "Simple steps to get a nice VS Code setup with linting hints and format on save"
date: 2017-08-19T11:04:59+02:00
updated: 2018-05-10T11:04:59+02:00
tags: react
---

This post explains the simple steps to get **a nice VS Code setup for React development**, with **linting hints** and **format on save**.

## ESLint

First, we're going to install ESLint. ESLint is an amazing tool that helps you keep your code tiny and clean.

Install [ESLint](/eslint/) using the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) available on the VS Code Extensions Store.

Then from the Terminal run those [Yarn](/yarn/) commands (if you don't have Yarn installed yet, follow the link to my tutorial to find a short guide):

```
yarn add babel-eslint
yarn add eslint-config-airbnb
yarn add eslint-plugin-jsx-a11y
yarn add eslint-plugin-react
```

Now, create a `.eslintrc.json` file in the root of your project, and add the following lines to have a basis ESLint configuration that works for React development, with [JSX](/jsx/) support:

```json
{
  "parser": "babel-eslint",
  "extends": "airbnb",
  "plugins": ["react", "jsx-a11y", "import"]
}
```

## Prettier

The next step I suggest is to install Prettier. [Prettier](/prettier/) is a JavaScript opinionated formatter. It's a great tool because it helps you standardize your codebase, and it's useful even if you code alone. In a team, it's super useful as it avoids differences in code styling. Use what Prettier suggests.

You can install [the Prettier VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) with [npm](/npm/):

```
npm install -g prettier-eslint --save-dev
```

Next we're going to add a few rules to the VS Code configuration, to apply Prettier on every save, and integrate it with ESLint. Press `cmd+,` (on Mac) and the VS Code configuration should show up. Enter this at the end:

```json
"editor.formatOnSave": true,
"javascript.format.enable": false,
"prettier.eslintIntegration": true
```
