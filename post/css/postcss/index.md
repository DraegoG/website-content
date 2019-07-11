---
title: "Introduction to PostCSS"
description: "Discover PostCSS, a great tool to help you write modern CSS. PostCSS is a very popular tool that allows developers to write CSS pre-processors or post-processors"
date: 2018-03-06T08:06:29+02:00
booktitle: PostCSS
tags: css
---

<!-- TOC -->

- [Introduction](#introduction)
- [Why it's so popular](#why-its-so-popular)
- [Install the PostCSS CLI](#install-the-postcss-cli)
- [Most popular PostCSS plugins](#most-popular-postcss-plugins)
  - [Autoprefixer](#autoprefixer)
  - [cssnext](#cssnext)
  - [CSS Modules](#css-modules)
  - [csslint](#csslint)
  - [cssnano](#cssnano)
  - [Other useful plugins](#other-useful-plugins)
- [How is it different than Sass?](#how-is-it-different-than-sass)

<!-- /TOC -->

## Introduction

PostCSS is a very popular tool that allows developers to write CSS pre-processors or post-processors, called **plugins**. There is a huge number of plugins that provide lots of functionalities, and sometimes the term "PostCSS" means the tool itself, plus the plugins ecosystem.

PostCSS plugins can be run via the command line, but they are generally invoked by task runners at build time.

The plugin-based architecture provides a common ground for all the CSS-related operations you need.

> Note: PostCSS despite the name is not a CSS post-processor, but it can be used to build them, as well as other things

## Why it's so popular

PostCSS provides several features that will *deeply improve your CSS*, and it integrates really well with any build tool of your choice.

## Install the PostCSS CLI

Using [Yarn](/yarn/):

```bash
yarn global add postcss-cli
```

or [npm](/npm/):

```bash
npm install -g postcss-cli
```

Once this is done, the `postcss` command will be available in your command line.

This command for example runs the autoprefixer plugin on CSS files contained in the css/ folder, and save the result in the main.css file:

```bash
postcss --use autoprefixer -o main.css css/*.css
```

More info on the PostCSS CLI here: <https://github.com/postcss/postcss-cli>.

## Most popular PostCSS plugins

PostCSS provides a common interface to several great tools for your CSS processing.

Here are some of the most popular plugins, to get an overview of what's possible to do with PostCSS.

### Autoprefixer

[Autoprefixer](https://github.com/postcss/autoprefixer) parses your CSS and determines if some rules need a vendor prefix.

It does so according to the [Can I Use](http://caniuse.com/) data, so you don't have to worry if a feature needs a prefix, or if prefixes you use are now unneeded because obsolete.

You get to write cleaner CSS.

Example:

```css
a {
    display: flex;
}
```

gets compiled to

```css
a {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
}
```

### cssnext

<https://github.com/MoOx/postcss-cssnext>

This plugin is the [Babel](/babel/) of CSS, allows you to use modern CSS features while it takes care of transpiling them to a CSS more digestible to older browsers:

- it adds prefixes using Autoprefixer (so if you use this, no need to use Autoprefixer directly)
- it allows you to use [CSS Variables](/css-variables/)
- it allows you to use nesting, like in Sass

and [a lot more](http://cssnext.io/features/)!

### CSS Modules

[CSS Modules](https://github.com/css-modules/postcss-modules) let you use CSS Modules.

CSS Modules are not part of the CSS standard, but they are a build step process to have scoped selectors.

### csslint

Linting helps you write correct CSS and avoid errors or pitfalls. The [stylint](http://stylelint.io/) plugin allows you to lint CSS at build time.

### cssnano

[cssnano](http://cssnano.co/) minifies your CSS and makes code optimizations to have the least amount of code delivered in production.

### Other useful plugins

On the PostCSS GitHub repo there is a [full list of the available plugins](https://github.com/postcss/postcss/blob/master/docs/plugins.md).

Some of the ones I like include:

- [LostGrid](https://github.com/peterramsing/lost) is a PostCSS grid system
- [postcss-sassy](https://github.com/andyjansson/postcss-sassy-mixins) provides Sass-like mixins
- [postcss-nested](https://github.com/postcss/postcss-nested) provides the ability to use Sass nested rules
- [postcss-nested-ancestors](https://github.com/toomuchdesign/postcss-nested-ancestors), reference any ancestor selector in nested CSS
- [postcss-simple-vars](https://github.com/postcss/postcss-simple-vars), use Sass-like variables
- [PreCSS](https://github.com/jonathantneal/precss) provides you many features of Sass, and this is what is most close to a complete Sass replacement

## How is it different than Sass?

Or any other CSS preprocessor?

The main benefit PostCSS provides over CSS preprocessors like Sass or Less is the ability to choose your own path, and cherry-pick the features you need, adding new capabilities at the same time. Sass or Less are "fixed", you get lots of features which you might or might not use, and you cannot extend them.

The fact that you "choose your own adventure" means that you can still use any other tool you like alongside PostCSS. You can still use Sass if this is what you want, and use PostCSS to perform other things that Sass can't do, like autoprefixing or linting.

You can write your own PostCSS plugin to do anything you want.