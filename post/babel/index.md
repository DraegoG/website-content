---
title: "A short and simple guide to Babel"
description: "Babel is an awesome entry in the Web Developer toolset. It's an awesome tool, and it’s been around for quite some time, but nowadays almost every JavaScript developer relies on it, and this will continue going on, because Babel is now indispensable and has solved a big problem for everyone."
date: 2018-02-13T09:07:49+02:00
updated: 2018-08-28T18:07:49+02:00
booktitle: "Babel"
tags: devtools
---

<!-- TOC -->

- [Introduction to Babel](#introduction-to-babel)
- [Installing Babel](#installing-babel)
- [An example Babel configuration](#an-example-babel-configuration)
- [Babel presets](#babel-presets)
  - [`env` preset](#env-preset)
  - [`react` preset](#react-preset)
  - [More info on presets](#more-info-on-presets)
- [Using Babel with webpack](#using-babel-with-webpack)

<!-- /TOC -->

> This article covers Babel 7, the current stable release

## Introduction to Babel

Babel is an awesome tool, and it’s been around for quite some time, but nowadays almost every [JavaScript](https://flaviocopes.com/javascript/) developer relies on it, and this will continue, because Babel is now indispensable and has solved a big problem for everyone.

Which problem?

The problem that every Web Developer has surely had: a feature of JavaScript is available in the latest release of a browser, but not in the older versions. Or maybe Chrome or Firefox implement it, but Safari iOS and Edge do not.

For example, ES6 introduced the **arrow function**:

```js
[1, 2, 3].map((n) => n + 1)
```

Which is now supported by all modern browsers. IE11 does not support it, nor Opera Mini (How do I know? By checking the [ES6 Compatibility Table](http://kangax.github.io/compat-table/es6/#test-arrow_functions)).

So how should you deal with this problem? Should you move on and leave those customers with older/incompatible browsers behind, or should you write older JavaScript code to make all your users happy?

Enter Babel. Babel is a **compiler**: it takes code written in one standard, and it transpiles it to code written into another standard.

You can configure Babel to transpile modern ES2017 JavaScript into JavaScript ES5 syntax:

```js
[1, 2, 3].map(function(n) {
  return n + 1
})
```

This must happen at build time, so you must setup a workflow that handles this for you. [Webpack](https://flaviocopes.com/webpack/) is a common solution.

(P.S. if all this _ES_ thing sounds confusing to you, see more about ES versions [in the ECMAScript guide](https://flaviocopes.com/ecmascript/))

## Installing Babel

Babel is easily installed using [npm](https://flaviocopes.com/npm/), locally in a project:

```bash
npm install --save-dev @babel/core @babel/cli
```

> In the past I recommended installing `babel-cli` globally, but this is now discouraged by the Babel maintainers, because by using it locally you can have different versions of Babel in each project, and also checking in babel in your repository is better for team work

Since npm now comes with [`npx`](https://flaviocopes.com/npx/), locally installed CLI packages can run by typing the command in the project folder:

So we can run Babel by just running

```bash
npx babel script.js
```

## An example Babel configuration

Babel out of the box does not do anything useful, you need to configure it and add plugins.

> [Here is a list of Babel plugins](https://babeljs.io/docs/en/plugins)

To solve the problem we talked about in the introduction (using arrow functions in every browser), we can run

```bash
npm install --save-dev \
    @babel/plugin-transform-es2015-arrow-functions
```

to download the package in the `node_modules` folder of our app, then we need to add

```js
{
  "plugins": ["transform-es2015-arrow-functions"]
}
```

to the `.babelrc` file present in the application root folder. If you don't have that file already, you just create a blank file, and put that content into it.

> TIP: If you have never seen a dot file (a file starting with a dot) it might be odd at first because that file might not appear in your file manager, as it's a hidden file.

Now if we have a `script.js` file with this content:

```js
var a = () => {};
var a = (b) => b;

const double = [1,2,3].map((num) => num * 2);
console.log(double); // [2,4,6]

var bob = {
  _name: "Bob",
  _friends: ["Sally", "Tom"],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
};
console.log(bob.printFriends());
```

running `babel script.js` will output the following code:

```js
var a = function () {};var a = function (b) {
  return b;
};

const double = [1, 2, 3].map(function (num) {
  return num * 2;
});console.log(double); // [2,4,6]

var bob = {
  _name: "Bob",
  _friends: ["Sally", "Tom"],
  printFriends() {
    var _this = this;

    this._friends.forEach(function (f) {
      return console.log(_this._name + " knows " + f);
    });
  }
};
console.log(bob.printFriends());
```

As you can see arrow functions have all been converted to JavaScript ES5 functions.

## Babel presets

We just saw in the previous article how Babel can be configured to transpile specific JavaScript features.

You can add much more plugins, but you can't add to the configuration features one by one, it's not practical.

This is why Babel offers **presets**.

The most popular presets are `env` and `react`.

> Tip: Babel 7 deprecated (and removed) yearly presets like `preset-es2017`, and stage presets. Use `@babel/preset-env` instead.

### `env` preset

The `env` preset is very nice: you tell it which environments you want to support, and it does everything for you, **supporting all modern JavaScript features**.

E.g. "support the last 2 versions of every browser, but for Safari let's support all versions since Safari 7`

```js
{
  "presets": [
    ["env", {
      "targets": {
        "browsers": ["last 2 versions", "safari >= 7"]
      }
    }]
  ]
}
```

or "I don't need browser support, just let me work with [Node.js](https://flaviocopes.com/nodejs/) 6.10"

```js
{
  "presets": [
    ["env", {
      "targets": {
        "node": "6.10"
      }
    }]
  ]
}
```

### `react` preset

The `react` preset is very convenient when writing React apps: adding `preset-flow`, `syntax-jsx`, `transform-react-jsx`, `transform-react-display-name`.

By including it, you are all ready to go developing React apps, with JSX transforms and Flow support.

### More info on presets

<https://babeljs.io/docs/plugins/>

## Using Babel with webpack


If you want to run modern JavaScript in the browser, Babel on its own is not enough, you also need to bundle the code. Webpack is the perfect tool for this.

> TIP: read the [webpack guide](https://flaviocopes.com/webpack/) if you're not familiar with webpack

Modern JS needs two different stages: a compile stage, and a runtime stage. This is because some ES6+ features need a polyfill or a runtime helper.

To install the Babel polyfill runtime functionality, run

```bash
npm install @babel/polyfill \
            @babel/runtime \
            @babel/plugin-transform-runtime
```

Now in your `webpack.config.js` file add:

```js
entry: [
  'babel-polyfill',
  // your app scripts should be here
],

module: {
  loaders: [
    // Babel loader compiles ES2015 into ES5 for
    // complete cross-browser support
    {
      loader: 'babel-loader',
      test: /\.js$/,
      // only include files present in the `src` subdirectory
      include: [path.resolve(__dirname, "src")],
      // exclude node_modules, equivalent to the above line
      exclude: /node_modules/,
      query: {
        // Use the default ES2015 preset
        // to include all ES2015 features
        presets: ['es2015'],
        plugins: ['transform-runtime']
      }
    }
  ]
}
```

By keeping the presets and plugins information inside the `webpack.config.js` file, we can avoid having a `.babelrc` file.
