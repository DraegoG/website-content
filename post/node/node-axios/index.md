---
title: "HTTP requests in Node using Axios"
description: "Axios is a very convenient JavaScript library to perform HTTP requests in Node.js"
date: 2018-08-21T07:00:00+02:00
updated: 2019-05-24T07:00:00+02:00
tags: node
tags_weight: 64
path: node-axios
---

<!-- TOC -->

- [Introduction](#introduction)
- [A video tutorial](#a-video-tutorial)
- [Installation](#installation)
- [The Axios API](#the-axios-api)
- [GET requests](#get-requests)
- [Add parameters to GET requests](#add-parameters-to-get-requests)
- [POST Requests](#post-requests)

<!-- /TOC -->

## Introduction

Axios is a very popular JavaScript library you can use to perform HTTP requests, that works in both Browser and [Node.js](https://flaviocopes.com/nodejs/) platforms.

![Axios](banner.png)

It supports all modern browsers, including support for IE8 and higher.

It is promise-based, and this lets us write async/await code to perform [XHR](https://flaviocopes.com/xhr/) requests very easily.

Using Axios has quite a few advantages over the native [Fetch API](https://flaviocopes.com/fetch-api/):

- supports older browsers (Fetch needs a polyfill)
- has a way to abort a request
- has a way to set a response timeout
- has built-in CSRF protection
- supports upload progress
- performs automatic JSON data transformation
- works in Node.js

## A video tutorial

Check out this video where I create an Express server that offers a POST endpoint, and I make an Axios request to it, to post data:

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/A5zZS1OUmmM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

## Installation

Axios can be installed using [npm](https://flaviocopes.com/npm/):

```bash
npm install axios
```

or [yarn](https://flaviocopes.com/yarn/):

```js
yarn add axios
```

or include it in your page using unpkg.com:

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

## The Axios API

You can start an HTTP request from the `axios` object:

> I use `foo` and `bar` as *random names*. Enter any kind of name to replace them.

```js
axios({
  url: 'https://dog.ceo/api/breeds/list/all',
  method: 'get',
  data: {
    foo: 'bar'
  }
})
```

but for convenience, you will generally use

- `axios.get()`
- `axios.post()`

(like in jQuery you would use `$.get()` and `$.post()` instead of `$.ajax()`)

Axios offers methods for all the HTTP verbs, which are less popular but still used:

- `axios.delete()`
- `axios.put()`
- `axios.patch()`
- `axios.options()`

and a method to get the HTTP headers of a request, discarding the body:

- `axios.head()`

## GET requests

One convenient way to use Axios is to use the modern (ES2017) async/await syntax.

This Node.js example queries the [Dog API](https://dog.ceo) to retrieve a list of all the dogs breeds, using `axios.get()`, and it counts them:

```js
const axios = require('axios')

const getBreeds = async () => {
  try {
    return await axios.get('https://dog.ceo/api/breeds/list/all')
  } catch (error) {
    console.error(error)
  }
}

const countBreeds = async () => {
  const breeds = await getBreeds()

  if (breeds.data.message) {
    console.log(`Got ${Object.entries(breeds.data.message).length} breeds`)
  }
}

countBreeds()
```

If you don't want to use async/await you can use the [Promises](https://flaviocopes.com/javascript-promises/) syntax:

```js
const axios = require('axios')

const getBreeds = () => {
  try {
    return axios.get('https://dog.ceo/api/breeds/list/all')
  } catch (error) {
    console.error(error)
  }
}

const countBreeds = async () => {
  const breeds = getBreeds()
    .then(response => {
      if (response.data.message) {
        console.log(
          `Got ${Object.entries(response.data.message).length} breeds`
        )
      }
    })
    .catch(error => {
      console.log(error)
    })
}

countBreeds()
```

## Add parameters to GET requests

A GET response can contain parameters in the URL, like this: `https://site.com/?foo=bar`.

With Axios you can perform this by using that URL:

```js
axios.get('https://site.com/?foo=bar')
```

or you can use a `params` property in the options:

```js
axios.get('https://site.com/', {
  params: {
    foo: 'bar'
  }
})
```

## POST Requests

Performing a POST request is just like doing a GET request, but instead of `axios.get`, you use `axios.post`:

```js
axios.post('https://site.com/')
```

An object containing the POST parameters is the second argument:

```js
axios.post('https://site.com/', {
  foo: 'bar'
})
```
