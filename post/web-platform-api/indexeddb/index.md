---
title: "Dive into IndexedDB"
date: 2018-02-28T09:06:15+02:00
updated: 2019-05-24T12:07:09+02:00
description: "IndexedDB is one of the storage capabilities introduced into browsers over the years. Here's an introduction to IndexedDB, the Database of the Web supported by all modern Browsers"
booktitle: "IndexedDB"
medium: true
tags: browser
---

<!-- TOC -->

- [Introduction to IndexedDB](#introduction-to-indexeddb)
- [Create an IndexedDB Database](#create-an-indexeddb-database)
  - [How to **create a database**](#how-to-create-a-database)
- [Adding data into a store](#adding-data-into-a-store)
  - [Adding data when the store is created, initializing it](#adding-data-when-the-store-is-created-initializing-it)
  - [Adding data when the store is already created, using transactions](#adding-data-when-the-store-is-already-created-using-transactions)
- [Getting data from a store](#getting-data-from-a-store)
  - [Getting one item from a store: `get()`](#getting-one-item-from-a-store-get)
  - [Getting all the items from a store: `getAll()`](#getting-all-the-items-from-a-store-getall)
- [Deleting data from IndexedDB](#deleting-data-from-indexeddb)
  - [Delete an entire IndexedDB database](#delete-an-entire-indexeddb-database)
  - [To delete data in an object store](#to-delete-data-in-an-object-store)
- [Migrate from previous version of a database](#migrate-from-previous-version-of-a-database)
- [Unique keys](#unique-keys)
  - [Check if a store exists](#check-if-a-store-exists)
- [Deleting from IndexedDB](#deleting-from-indexeddb)
  - [Delete a database](#delete-a-database)
  - [Delete an object store](#delete-an-object-store)
  - [To delete data in an object store use a transaction](#to-delete-data-in-an-object-store-use-a-transaction)
- [There's more!](#theres-more)

<!-- /TOC -->

## Introduction to IndexedDB

IndexedDB is one of the storage capabilities introduced into browsers over the years.
It's a key/value store (a noSQL database) considered to be **the definitive solution for storing data in browsers**.

It's an asynchronous API, which means that performing costly operations won't block the UI thread providing a sloppy experience to users. It can store an indefinite amount of data, although once over a certain threshold the user is prompted to give the site higher limits.

It's [supported on all modern browsers](http://caniuse.com/#feat=indexeddb).

It supports transactions, versioning and gives good performance.

Inside the browser we can also use:

- [**Cookies**](/cookies/): can host a very small amount of strings
- [**Web Storage**](/web-storage-api/) (or DOM Storage), a term that commonly identifies localStorage and  sessionStorage, two key/value stores. sessionStorage, does not retain data, which is cleared when the session ends, while localStorage keeps the data across sessions

Local/session storage have the disadvantage of being capped at a small (and inconsistent) size, with browsers implementation offering from 2MB to 10MB of space per site.

In the past we also had **Web SQL**, a wrapper around SQLite, but now this is **deprecated** and unsupported on some modern browsers, it's never been a recognized standard and so it should not be used, although 83% of users have this technology on their devices [according to Can I Use](http://caniuse.com/#feat=sql-storage).

While you can technically create multiple databases per site, you generally **create one single database**, and inside that database you can create **multiple object stores**.

A database is **private to a domain**, so any other site cannot access another website IndexedDB stores.

Each store usually contains a set of _things_, which can be

- strings
- numbers
- objects
- arrays
- dates

> For example you might have a store that contains posts, another that contains comments.

A store contains a number of items which have a unique key, which represents the way by which an object can be identified.

You can alter those stores using transactions, by performing add, edit and delete operations, and iterating over the items they contain.

Since the advent of [Promises](/javascript-promises) in ES6, and the subsequent move of APIs to using promises, the IndexedDB API seems a bit _old school_.

While there's nothing wrong in it, in all the examples that I'll explain I'll use the [IndexedDB Promised Library](https://github.com/jakearchibald/idb) by Jake Archibald, which is a tiny layer on top of the IndexedDB API to make it easier to use.

> This library is also used on all the examples on the Google Developers website regarding IndexedDB

## Create an IndexedDB Database

The simplest way is to use *unpkg*, by adding this to the page header:

```html
<script type="module">
import { openDB, deleteDB } from 'https://unpkg.com/idb?module'
</script>
```

Before using the IndexedDB API, always make sure you check for support in the browser, even though it's widely available, you never know which browser the user is using:

```js
(() => {
  'use strict'

  if (!('indexedDB' in window)) {
    console.warn('IndexedDB not supported')
    return
  }

  //...IndexedDB code
})()
```

### How to **create a database**

Using `openDB()`:

```js
(async () => {
  //...

  const dbName = 'mydbname'
  const storeName = 'store1'
  const version = 1 //versions start at 1

  const db = await openDB(dbName, version, {
    upgrade(db, oldVersion, newVersion, transaction) {
      const store = db.createObjectStore(storeName)
    }
  })
})()
```

The first 2 parameters are the database name, and the verson. The third param, which is optional, is an object that contains a function **called only if the version number is higher than the current installed database version**. In the function body you can upgrade the structure (stores and indexes) of the db.

## Adding data into a store

### Adding data when the store is created, initializing it

You use the `put` method of the object store, but first we need a reference to it, which we can get from `db.createObjectStore()` when we create it.

When using `put`, the value is the first argument, the key is the second. This is because if you specify `keyPath` when creating the object store, you don't need to enter the key name on every put() request, you can just write the value.

This populates `store0` as soon as we create it:

```js
(async () => {
  //...
  const dbName = 'mydbname'
  const storeName = 'store0'
  const version = 1

  const db = await openDB(dbName, version,{
    upgrade(db, oldVersion, newVersion, transaction) {
      const store = db.createObjectStore(storeName)
      store.put('Hello world!', 'Hello')
    }
  })
})()
```

### Adding data when the store is already created, using transactions

To add items later down the road, you need to create a read/write **transaction**, that ensures database integrity (if an operation fails, all the operations in the transaction are rolled back and the state goes back to a known state).

For that, use a reference to the `dbPromise` object we got when calling `openDB`, and run:

```js
(async () => {
  //...
  const dbName = 'mydbname'
  const storeName = 'store0'
  const version = 1

  const db = await openDB(/* ... */)

  const tx = db.transaction(storeName, 'readwrite')
  const store = await tx.objectStore(storeName)

  const val = 'hey!'
  const key = 'Hello again'
  const value = await store.put(val, key)
  await tx.done
})()
```


## Getting data from a store

### Getting one item from a store: `get()`

```js
const key = 'Hello again'
const item = await db.transaction(storeName).objectStore(storeName).get(key)
```

### Getting all the items from a store: `getAll()`

Get all the keys stored

```js
const items = await db.transaction(storeName).objectStore(storeName).getAllKeys()
```

Get all the values stored

```js
const items = await db.transaction(storeName).objectStore(storeName).getAll()
```

## Deleting data from IndexedDB

Deleting the database, an object store and data

### Delete an entire IndexedDB database

```js
const dbName = 'mydbname'
await deleteDB(dbName)
```

### To delete data in an object store

We use a transaction:

```js
(async () => {
  //...

  const dbName = 'mydbname'
  const storeName = 'store1'
  const version = 1

  const db = await openDB(dbName, version, {
    upgrade(db, oldVersion, newVersion, transaction) {
      const store = db.createObjectStore(storeName)
    }
  })

  const tx = await db.transaction(storeName, 'readwrite')
  const store = await tx.objectStore(storeName)

  const key = 'Hello again'
  await store.delete(key)
  await tx.done
})()
```


## Migrate from previous version of a database

The third (optional) parameter of the `openDB()` function is an object that can contain an `upgrade` function **called only if the version number is higher than the current installed database version**. In that function body you can upgrade the structure (stores and indexes) of the db:

```js
const name = 'mydbname'
const version = 1
openDB(name, version, {
  upgrade(db, oldVersion, newVersion, transaction) {
    console.log(oldVersion)
  }
})
```

In this callback, you can check from which version the user is updating, and perform some operations accordingly.

You can perform a migration from a previous database version using this syntax

```js
(async () => {
  //...
  const dbName = 'mydbname'
  const storeName = 'store0'
  const version = 1

  const db = await openDB(dbName, version, {
    upgrade(db, oldVersion, newVersion, transaction) {
      switch (oldVersion) {
        case 0: // no db created before
          // a store introduced in version 1
          db.createObjectStore('store1')
        case 1:
          // a new store in version 2
          db.createObjectStore('store2', { keyPath: 'name' })
      }
      db.createObjectStore(storeName)
    }
  })
})()
```


## Unique keys

`createObjectStore()` as you can see in `case 1` accepts a second parameter that indicates the index key of the database. This is very useful when you store objects: `put()` calls don't need a second parameter, but can just take the value (an object) and the key will be mapped to the object property that has that name.

The index gives you a way to retrieve a value later by that specific key, and it must be unique (every item must have a different key)

A key can be set to auto increment, so you don't need to keep track of it on the client code:

```js
db.createObjectStore('notes', { autoIncrement: true })
```

Use auto increment if your values do not contain a unique key already (for example, if you collect email addresses without an associated name).

### Check if a store exists

You can check if an object store already exists by calling the `objectStoreNames()` method:

```js
const storeName = 'store1'

if (!db.objectStoreNames.contains(storeName)) {
  db.createObjectStore(storeName)
}
```

## Deleting from IndexedDB

Deleting the database, an object store and data

### Delete a database

```js
await deleteDB('mydb')
```

### Delete an object store

An object store can only be deleted in the callback when opening a db, and that callback is only called if you specify a version higher than the one currently installed:

```js
const db = await openDB('dogsdb', 2, {
  upgrade(db, oldVersion, newVersion, transaction) {
    switch (oldVersion) {
      case 0: // no db created before
        // a store introduced in version 1
        db.createObjectStore('store1')
      case 1:
        // delete the old store in version 2, create a new one
        db.deleteObjectStore('store1')
        db.createObjectStore('store2')
    }
  }
})
```

### To delete data in an object store use a transaction

```js
const key = 232 //a random key

const db = await openDB(/*...*/)
const tx = await db.transaction('store', 'readwrite')
const store = await tx.objectStore('store')
await store.delete(key)
await tx.complete
```

## There's more!

These are just the basics. I didn't talk about cursors and more advanced stuff. There's more to IndexedDB but I hope this gives you a head start.