---
title: "Using Tailwind with Vue.js"
description: This article explains how to set up Tailwind for usage in a Vue CLI 3 project
date: 2018-06-26T07:04:59+02:00
tags: vue
---

[Tailwind](https://tailwindcss.com/) is a pretty cool CSS framework.

In this post I'm going to show you how to use it on a Vue app.

It's 4 simple steps:

<!-- TOC -->

- [Install Tailwind](#install-tailwind)
- [Create a configuration file](#create-a-configuration-file)
- [Configure PostCSS](#configure-postcss)
- [Create a CSS file](#create-a-css-file)
- [Import the file in your Vue app](#import-the-file-in-your-vue-app)
- [Testing it works fine](#testing-it-works-fine)

<!-- /TOC -->

In this post I assume the project you want to use Tailwind on is based on Vue CLI 3.

## Install Tailwind

First step is to install Tailwind, using npm or yarn:

```bash
# Using npm
npm install tailwindcss --save-dev

# Using Yarn
yarn add tailwindcss --dev
```

## Create a configuration file

Next, use the Tailwind command that is provided to create a configuration file.

```bash
./node_modules/.bin/tailwind init tailwind.js
```

This will create a `tailwind.js` file in the root of your project, adding the basic Tailwind configuration. The file is very long, and I won't paste it here, but it contains lots of presets that will be very useful later.

## Configure PostCSS

Now you need to tweak the [PostCSS](/postcss/) configuration to make sure Tailwind runs. Add:

```js
module.exports = {
  "plugins": [
    require('tailwindcss')('tailwind.js'),
    require('autoprefixer')(),
  ]
}
```

to your `postcss.config.js`. Create one if it does not exist.

Note: if you set Vue CLI to store the configuration in `package.json`, make sure no PostCSS configuration lies in that file. By default Vue CLI adds these lines:

```json
  "postcss": {
    "plugins": {
      "autoprefixer": {}
    }
  },
```

**remove them**, or the `postcss.config.js` file won't be read.

## Create a CSS file

Now create a CSS file in `src/assets/css/tailwind.css` and add

```css
@tailwind preflight;
@tailwind components;
@tailwind utilities;
```

## Import the file in your Vue app

Import tailwind in main.js:

```js
import '@/assets/css/tailwind.css'
```

(`@` in vue points to `src/`)

That's it! Now restart your Vue CLI project and it should all work fine.

## Testing it works fine

You won't notice anything unless you add Tailwind-specific classes.

Try for example adding this HTML in one of your templates:

```html
<div class="bg-purple text-white sm:bg-green md:bg-blue md:text-yellow lg:bg-red xl:bg-orange ...">
  Test
</div>
```

That should create a colored box.