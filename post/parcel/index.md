---
title: "Parcel, a simpler webpack"
seotitle: "Parcel Tutorial: learn the simpler webpack"
date: 2018-06-24T07:06:15+02:00
description: "Parcel is a Web Application Bundler. It's in the same tool category of webpack, with a different value proposition. Parcel promises to do many things without any configuration at all, and be fast too."
booktitle: "Parcel"
tags: devtools
---

Parcel is a Web Application Bundler.

It's in the same tool category of [webpack](/webpack/), with a different value proposition.

Its main features set includes

- assets bundling (JS, CSS, HTML, images)
- zero config code splitting
- automatic transforms using [Babel](/babel/), [PostCSS](/postcss/) and PostHTML
- hot module replacement
- caching and parallel processing for faster builds

Parcel promises to do all of this without any configuration at all, and be fast too.

## Installation

Parcel is installed using [Yarn](/yarn/):

```js
yarn global add parcel-bundler
```

or [npm](/npm/):

```js
npm install -g parcel-bundler
```

## Start Parcel

Parcel can be started using

```bash
parcel watch index.html
```

it will start scanning for assets from the HTML page source, and substitute any of the references it processes, with an output file.

You can also point Parcel to a JS file instead:

```bash
parcel watch entry.js
```

### Development server

Conveniently Parcel comes with a built-in development server, so you don't have to set up one. You can start it with:

```bash
parcel index.html
```

### Production-ready bundle

When you're happy with your app and you want to create a production-ready bundle, run

```bash
parcel build index.html
```

A production bundle disables hot module replacement and does not watch your changes, it exists once the bundling is done, and uses a minifier.

It also automatically trigger the `NODE_ENV` variable to `production`, to make libraries generate the production code (e.g. React and [Vue](/vue-introduction/) use this convention)

## Assets

### JavaScript

Parcel supports both **ES Modules** (`import...`) and **CommonJS** (`require...`).

It performs **automatic Code Splitting using dynamic imports**.

What does this mean, and why is this useful?

A dynamic import returns a [promise](/javascript-promises/), and instead of loading all the dependencies at the application start, we can ask the browser to load them, but only executes some parts of the app when they are ready.

Or, we can ask the browser to load them only when we need it, for example when the user clicks a particular link.

See [code splitting](https://parceljs.org/code_splitting.html) for more details.

### CSS

Parcel supports plain CSS, Sass, Less and Stylus.

You can write your CSS using [CSS Modules](https://github.com/css-modules/css-modules).

## Transforms

When Parcel finds you have a configuration for one of

- Babel (`.babelrc`)
- PostCSS (`.postcssrc`)
- PostHTML (`.posthtmlrc`)

it will use that automatically in its bundling process.

## Hot module replacement

Hot module replacement (HMR) is a useful feature when building an application. When we save a new copy of CSS or JavaScript, HMR takes care of updating the module in the browser, without refreshing the whole application.

This is cool especially if your application has lots of states you need to trigger to test a specific functionality (e.g. "go to settings, click this, type that...").

## Parcel vs webpack

Let's compare Parcel to webpack, because that's so popular and you have probably heard of it or used it in a project. It's also nice to know the differences even if you never used any of them.

webpack allows you to do tons of things, and while this is very cool, also means that we need to carefully configure it to do exactly what we want.

Sometimes the `webpack.config.js` file grows to hundreds of lines, and we copy/paste it to the next project, and it's a pain if we need to modify it.

Parcel promises us to do a lot of what webpack does, but **without any configuration at all**, relying on **conventions over configuration**.

> webpack 4, mostly in response to the Parcel success, introduced a zero-config mode, with some conventions, rather than always requiring a configuration.

While webpack has [thousands of plugins](https://www.npmjs.com/search?q=webpack-plugin), Parcel has [some](https://www.npmjs.com/search?q=parcel-plugin), but they are not advertised on the site, a sign that developers of Parcel want us to avoid using plugins until we can't really avoid them because we can't adapt to the conventions of Parcel, or to make Parcel support something that it does not out of the box.

**Which one should you use?** I would recommend Parcel for small projects, and webpack when you grow out of its capabilities and you want absolute control on everything your module bundler does.
