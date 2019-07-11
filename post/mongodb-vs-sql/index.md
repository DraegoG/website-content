---
title: "How MongoDB is different from a SQL database"
date: 2018-11-23T07:00:00+02:00
description: "Generally speaking there are 2 major types of databases: SQL databases, and NoSQL databases"
---

If you are familiar with MySQL or PostgreSQL for example, SQL databases allow you to add and retrieve data using a specific language, called SQL, that looks like this:

```sql
SELECT * FROM cars
INSERT INTO cars VALUES (fiesta, 2010)
```

SQL is rather old, being born in 1986, and it's a battle-tested technology.

Under the *NoSQL* umbrella we put all those databases that do not use the SQL language for querying the data.

MongoDB falls under this umbrella.

MongoDB is a **document database**. Instead of storing records, we store objects (called *documents*).

How does this differ from a SQL database? Tables in a SQL database are *flat* and *static*, they can host data but limited to what the original intent was (you can't add a column dynamically) and to store complex data you need to create many tables and link the data in each table, following the relational databases common practices (like foreign keys, column types, etc).

In MongoDB you can store any object without having to worry about the particular fields that compose this object and how to store them. You tell MongoDB to store that object.

With MongoDB, you don't need to learn another language to interact with the data: you just call the JavaScript methods it exposes and that's it (of course you can interact with it using other languages as well).

Data is stored in a format similar to JSON, but enhanced to allow storing more than just basic data types.

I hope this gives you a brief overview of the key differences between SQL databases and MongoDB.