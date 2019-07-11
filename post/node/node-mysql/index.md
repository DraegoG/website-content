---
title: The basics of working with MySQL and Node
description: "MySQL is one of the most popular relational databases in the world. Find out how to make it work with Node.js"
date: 2018-08-28T07:00:00+02:00
tags: node
tags_weight: 70
path: node-mysql
---

MySQL is one of the most popular relational databases in the world.

The Node ecosystem of course has several different packages that allow you to interface with MySQL, store data, retrieve data, and so on.

We'll use [`mysqljs/mysql`](https://github.com/mysqljs/mysql), a package that has over 12.000 GitHub stars and has been around for years.

## Installing the Node mysql package

You install it using

```bash
npm install mysql
```

## Initializing the connection to the database

You first include the package:

```js
const mysql = require('mysql')
```

and you create a connection:

```js
const options = {
  user: 'the_mysql_user_name',
  password: 'the_mysql_user_password',
  database: 'the_mysql_database_name'
}
const connection = mysql.createConnection(options)
```

You initiate a new connection by calling:

```js
connection.connect(err => {
  if (err) {
    console.error('An error occurred while connecting to the DB')
    throw err
  }
})
```

## The connection options

In the above example, the `options` object contained 3 options:

```js
const options = {
  user: 'the_mysql_user_name',
  password: 'the_mysql_user_password',
  database: 'the_mysql_database_name'
}
```

There are many more you can use, including:

- `host`, the database hostname, defaults to `localhost`
- `port`, the MySQL server port number, defaults to 3306
- `socketPath`, used to specify a unix socket instead of host and port
- `debug`, by default disabled, can be used for debugging
- `trace`, by default enabled, prints stack traces when errors occur
- `ssl`, used to setup an SSL connection to the server (out of the scope of this tutorial)

## Perform a SELECT query

Now you are ready to perform a SQL query on the database. The query once executed will invoke a callback function which contains an eventual error, the results and the fields.

```js
connection.query('SELECT * FROM todos', (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
```

You can pass in values which will be automatically escaped:

```js
const id = 223
connection.query('SELECT * FROM todos WHERE id = ?', [id], (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
```

To pass multiple values, just put more elements in the array you pass as the second parameter:

```js
const id = 223
const author = 'Flavio'
connection.query('SELECT * FROM todos WHERE id = ? AND author = ?', [id, author], (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
```

## Perform an INSERT query

You can pass an object

```js
const todo = {
  thing: 'Buy the milk'
  author: 'Flavio'
}
connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
})
```

If the table has a primary key with `auto_increment`, the value of that will be returned in the `results.insertId` value:

```js
const todo = {
  thing: 'Buy the milk'
  author: 'Flavio'
}
connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }}
  const id = results.resultId
  console.log(id)
)
```

## Close the connection

When you need to terminate the connection to the database you can call the `end()` method:

```js
connection.end()
```

This makes sure any pending query gets sent, and the connection is gracefully terminated.
