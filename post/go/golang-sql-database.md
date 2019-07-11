---
title: "Working with a SQL Database in Go"
date: 2017-08-14T15:46:52+02:00
tags: go
---

In this article I list how to do common SQL database operations with Go.

<!-- TOC -->

- [Introducing `database/sql`](#introducing-databasesql)
- [Open the database connection](#open-the-database-connection)
- [Close the database connection](#close-the-database-connection)
- [Extract data from the database](#extract-data-from-the-database)
    - [Select a single row](#select-a-single-row)
    - [Select multiple rows](#select-multiple-rows)

<!-- /TOC -->

## Introducing `database/sql`

Go offers a clean SQL database API in its standard library `database/sql` package, but the specific database drivers must be installed separately.

It's a smart approach because it provides a common interface that nearly every DB driver implements.

If you want to use MySQL, you can use <https://github.com/go-sql-driver/mysql>.

If you're using Postgres, use <https://github.com/lib/pq>.

You just need to include the lib using `import _`, and the `database/sql` API will be configured to enable that driver:

```go
import "database/sql"
import _ "github.com/go-sql-driver/mysql"
```

## Open the database connection

Although the goal is to have it abstracted, there are still differences in some things, for example in how you connect to a database:

```go
import "database/sql"
import _ "github.com/go-sql-driver/mysql"

//...

db, err := sql.Open("mysql", "theUser:thePassword@/theDbName")
if err != nil {
  panic(err)
}
```

```go
import "database/sql"
import _ "github.com/lib/pq"

//...

db, err := sql.Open("postgres", "user=theUser dbname=theDbName sslmode=verify-full")
if err != nil {
  panic(err)
}
```

but much of the actual API is db-independent, and can be interchanged quite easily (not talking about SQL here, just referring to the database API).

## Close the database connection

Where it makes sense, you should always close the database connection.

You can as usual use `defer` to close it when the function that opens the db connection ends:

```go
db, err := sql.Open("postgres", psqlInfo)
defer db.Close()
```

## Extract data from the database

### Select a single row

Querying a table is done in 2 steps. First you call `db.QueryRow()`, then you call `Scan()` on the result.

Example:

```go
id := 1
var col string
sqlStatement := `SELECT col FROM my_table WHERE id=$1`
row := db.QueryRow(sqlStatement, id)
err := row.Scan(&col)
if err != nil {
    if err == sql.ErrNoRows {
        fmt.Println("Zero rows found")
    } else {
        panic(err)
    }
}
```

[`db.QueryRow()`](https://golang.org/pkg/database/sql/#DB.QueryRow) is used to query a single value from a table.

Signature:

> `func (db *DB) QueryRow(query string, args ...interface{}) *Row`

It returns a pointer to a [`db.Row`](https://golang.org/pkg/database/sql/#Row) value.

[`(*Row) Scan`](https://golang.org/pkg/database/sql/#Row.Scan) scans the row, copying the column values to the parameter passed into it.

Signature:

> `func (r *Row) Scan(dest ...interface{}) error`

**If more than one row was returned, it only scans the first one** and ignore the rest.

**If no row was returned, it returns a `ErrNoRows` error**.

> `var ErrNoRows = errors.New("sql: no rows in result set")`

### Select multiple rows

To query a single row we used `db.QueryRow()`. To query multiple rows we use `db.Query()`, which returns a `*Rows` value.

From the docs:

```go
//Rows is the result of a query. Its cursor starts before  the first row of the result set. Use Next to advance through the rows:

    rows, err := db.Query("SELECT ...")
    ...
    defer rows.Close()
    for rows.Next() {
        var id int
        var name string
        err = rows.Scan(&id, &name)
        ...
    }
     err = rows.Err() // get any error encountered ing iteration
    ...
```
// Err returns the error, if any, that was encountered during iteration.
// Err may be called after an explicit or implicit Close.


We need to iterate on `rows.Next()`, which allows us to call `rows.Scan()` into the loop.

If any error arises when preparing the next row, the loop ends and we can get the error by calling `rows.Err()`:

```go
type Timeline struct {
    Id int
    Content string
}
rows, err := db.Query(`SELECT id, content FROM timeline`)
if err != nil {
    panic(err)
}
defer rows.Close()
for rows.Next() {
    timeline := Timeline{}
    err = rows.Scan(&timeline.Id, &timeline.Content)
    if err != nil {
        panic(err)
    }
    fmt.Println(timeline)
}
err = rows.Err()
if err != nil {
    panic(err)
}
```
