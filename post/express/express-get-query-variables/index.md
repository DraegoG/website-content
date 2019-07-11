---
title: Retrieve the GET query string parameters using Express
seotitle: How to retrieve the GET query string parameters using Express
description: "The query string is the part that comes after the URL path, and starts with a question mark. Let's see how to get the properties values."
date: 2018-08-06T15:00:00+02:00
tags: express
tags_weight: 17
path: express-get-query-variables
---

The query string is the part that comes after the URL path, and starts with a question mark `?`.

Example:

```txt
?name=flavio
```

Multiple query parameters can be added using `&`:

```txt
?name=flavio&age=35
```

How do you get those query string values in Express?

Express makes it very easy by populating the `Request.query` object for us:

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  console.log(req.query)
})

app.listen(8080)
```

This object is filled with a property for each query parameter.

If there are no query params, it's an empty object.

This makes it easy to iterate on it using the for...in loop:

```js
for (const key in req.query) {
  console.log(key, req.query[key])
}
```

This will print the query property key and the value.

You can access single properties as well:

```js
req.query.name //flavio
req.query.age //35
```