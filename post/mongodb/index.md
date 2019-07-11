---
title: "The MongoDB basics tutorial"
date: 2018-11-22T07:00:00+02:00
description: "MongoDB is a database, the part of the application responsible for storing and retrieving information."
---

MongoDB is a NoSQL database. Under the *NoSQL* umbrella we put all those databases that do not use the SQL language for querying the data.

## Key characteristics of MongoDB

MongoDB is a very JavaScript-friendly database. It exposes a JavaScript API we can use to create databases and collections of objects (called *documents*).

It's *schemaless*, which means you don't need to pre-define a structure for the data before storing it.

In MongoDB you can store any object without having to worry about the particular fields that compose this object and how to store them. You tell MongoDB to store that object.

Data is stored in a format similar to JSON, but enhanced to allow storing more than just basic data types.

## Installation

Let's go ahead and install MongoDB. You could use one of the many cloud providers that offer access to a MongoDB instance, but for the sake of learning, we'll install it ourselves.

I use a Mac, so the installation instructions in this tutorial refer to that operating system.

Open the terminal and run:

```bash
brew install mongodb
```

That's it.

The instructions were not too long or complicated, assuming you know how to use the terminal and [how to install Homebrew](https://brew.sh/).

The installation tells us this:

```
To have launchd start mongodb now and restart at login:
  brew services start mongodb
Or, if you don't want/need a background service you can just run:
  mongod --config /usr/local/etc/mongod.conf
```

You can choose to either launch MongoDB once and have it running forever as a background service in your computer (the thing I prefer), or you can run it just when you need it, by running the latter command.

The default configuration for MongoDB is this:

```
systemLog:
  destination: file
  path: /usr/local/var/log/mongodb/mongo.log
  logAppend: true
storage:
  dbPath: /usr/local/var/mongodb
net:
  bindIp: 127.0.0.1
```

Logs are stored in `/usr/local/var/log/mongodb/mongo.log` and the database is stored in `/usr/local/var/mongodb`.

By default there is no access control, anyone can read and write to the database.

## The Mongo Shell

The best way to experiment with MongoDB and starting to interact with it is by running the `mongo` program, which starts the MongoDB shell.

![](Screen%20Shot%202018-11-02%20at%2007.48.30.png)

You can now enter any command that Mongo understands.

## Create a database

When you start, Mongo creates a database called `test`. Run `db` in the shell to tell you the name of the active database

![](Screen%20Shot%202018-11-02%20at%2009.01.03.png)

To change the database, just write `use newname` and the `newname` database will be instantly created and the shell switches to using that.

![](Screen%20Shot%202018-11-02%20at%2009.02.30.png)

Use `show databases` to list the available databases:

![](Screen%20Shot%202018-11-02%20at%2009.03.31.png)

As you can see, the `something` database is not listed, just because there is no collection yet in it. Let's create one.

## Collections

In MongoDB, a **collection** is the equivalent of a SQL database table.

You create a collection on the current database by using the `db.createCollection()` command. The first argument is the database name, and you can pass an options object as a second parameter.

![](Screen%20Shot%202018-11-02%20at%2009.06.28.png)

Once you do so, `show databases` will list the new database, and `show collections` will list the collection.

![](Screen%20Shot%202018-11-02%20at%2009.05.13.png)

You can also create a new collection by using it as a property of the `db` object, and calling `insert()` to add an object to the collection:

```js
db.dogs.insert({ name: 'Roger' })
```

![](Screen%20Shot%202018-11-02%20at%2009.08.12.png)

## Listing objects in a collection

To show the objects added to a collection, use the `find()` method:

![](Screen%20Shot%202018-11-02%20at%2009.09.12.png)

As you can see there is an additional `_id` property for the record we added. That's automatically generated for us by MongoDB.

Now, add more dogs:

```js
db.dogs.insert({ name: 'Buck' })
db.dogs.insert({ name: 'Togo' })
db.dogs.insert({ name: 'Balto' })
```

Calling `db.dogs.find()` will give us all the entries, while we can pass a parameter to filter and retrieve a specific entry, for example with `db.dogs.find({name: 'Roger'})`:

![](Screen%20Shot%202018-11-02%20at%2009.11.35.png)

The `find()` method returns a cursor you need to iterate on.

There is another method which is handy when you know you'll only get one record, which is `findOne()`, and it's used in the same way. If multiple records match a query, it will just return the first one.

![](Screen%20Shot%202018-11-02%20at%2009.30.40.png)

## Updating records

To update a record you can use the `update()` method on a collection:

![](Screen%20Shot%202018-11-02%20at%2009.36.38.png)

## Removing records

You can remove a record calling the `remove()` method on a collection, passing an object to help identify it:

![](Screen%20Shot%202018-11-02%20at%2009.37.56.png)

To remove all the entries from a collection, pass an empty object:

```js
db.dogs.remove({})
```
