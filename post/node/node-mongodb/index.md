---
title: How to use MongoDB with Node.js
description: "In this tutorial I'll show you how to interact with a MongoDB database from Node.js"
date: 2018-11-24T07:00:00+02:00
tags: node
---

> If you are unfamiliar with [MongoDB](/mongodb/) check our guide on its basics and on how to install and use it :)

We'll be using the official `mongodb` [npm](/npm/) package. If you already have a Node.js project you are working on, install it using

```bash
npm install mongodb
```

If you start from scratch, create a new folder with your [terminal](/macos-terminal/) and run `npm init` to start up a new Node.js project, and then run the `npm install mongodb` command.

## Connecting to MongoDB

You require the `mongodb` package and you get the MongoClient object from it.

```js
const mongo = require('mongodb').MongoClient
```

Create a URL to the MongoDB server. If you use MongoDB locally, the URL will be something like `mongodb://localhost:27017`, as `27017` is the default port.

```js
const url = 'mongodb://localhost:27017'
```

Then use the `mongo.connect()` method to get the reference to the MongoDB instance client:

```js
mongo.connect(url, (err, client) => {
  if (err) {
    console.error(err)
    return
  }
  //...
})
```

Now you can select a database using the `client.db()` method:

```js
const db = client.db('kennel')
```

## Create and get a collection

You can get a collection by using the `db.collection()` method. If the collection does not exist yet, it's created.

```js
const collection = db.collection('dogs')
```

## Insert data into a collection a Document

Add to app.js the following function which uses the `insertOne()` method to add an object `dogs` collection.

```js
collection.insertOne({name: 'Roger'}, (err, result) => {

})
```

You can add multiple items using `insertMany()`, passing an array as the first parameter:

```js
collection.insertMany([{name: 'Togo'}, {name: 'Syd'}], (err, result) => {

})
```

## Find all documents

Use the `find()` method on the collection to get all the documents added to the collection:

```js
collection.find().toArray((err, items) => {
  console.log(items)
})
```

## Find a specific document

Pass an object to the `find()` method to filter the collection based on what you need to retrieve:

```js
collection.find({name: 'Togo'}).toArray((err, items) => {
  console.log(items)
})
```

If you know you are going to get one element, you can skip the `toArray()` conversion of the cursor by calling `findOne()`:

```js
collection.findOne({name: 'Togo'}, (err, item) => {
  console.log(item)
})
```

## Update an existing document

Use the `updateOne()` method to update a document:

```js
collection.updateOne({name: 'Togo'}, {'$set': {'name': 'Togo2'}}, (err, item) => {
  console.log(item)
})
```

## Delete a document

Use the `deleteOne()` method to delete a document:

```js
collection.deleteOne({name: 'Togo'}, (err, item) => {
  console.log(item)
})
```

## Closing the connection

Once you are done with the operations you can call the `close()` method on the client object:

```js
client.close()
```

## Use promises or async/await

I posted all those examples using the [callback](/javascript-callbacks/) syntax. This API supports [promises](/javascript-promises/) (and [async/await](/javascript-async-await/)) as well.

For example this

```js
collection.findOne({name: 'Togo'}, (err, item) => {
  console.log(item)
})
```

Can be used with promises:

```js
collection.findOne({name: 'Togo'})
  .then(item => {
    console.log(item)
  })
  .catch(err => {
  console.error(err)
  })
```

or async/await:

```js
const find = async () => {
  try {
    const item = await collection.findOne({name: 'Togo'})
  } catch(err => {
  console.error(err)
  })
}

find()
```