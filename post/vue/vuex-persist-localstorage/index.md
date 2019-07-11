---
title: Store Vue data to localStorage using Vuex
description: "Learn how to store Vuex data automatically to localStorage or sessionStorage"
date: 2018-07-11T07:04:59+02:00
tags: vue
---

When talking about storing data, there are various ways to persist data.

One is very simple, it's perfect for prototypes, and it's storing the data using the [Web Storage API](https://flaviocopes.com/web-storage-api/): localStorage and sessionStorage.

Using Vue you can make use of that API in many ways. One of the simplest ones is to rely on the [`vuex-persist`](https://github.com/championswimmer/vuex-persist) library.

You install it using npm or Yarn:

```bash
npm install vuex-persist

#or
yarn add vuex-persist
```

Open the Vuex store file, and add:

```js
import VuexPersist from 'vuex-persist'
```

Initialize VuexPersist:

```js
const vuexPersist = new VuexPersist({
  key: 'my-app',
  storage: localStorage
})
```

`key` is the key that's used in the localStorage database.

Change `localStorage` with `sessionStorage` to use that other storage system (each has its own peculiarities, see the Web Storage API document I linked above).

Next up, add `vuexPersist` to the list of Vuex plugins, when initializing the store:

```js
const store = new Vuex.Store({
  //...initialization
  plugins: [vuexPersist.plugin]
})
```

That's it! Any time the store is changed, the library will persist it to the browser.

There are more advanced capabilities you can find out on the [official documentation](https://github.com/championswimmer/vuex-persist), but these are the basics to get you started.