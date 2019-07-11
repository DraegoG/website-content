---
title: How to read environment variables from Node.js
description: "Learn how to read and make use of environment variables in a Node.js program"
date: 2018-09-10T07:00:00+02:00
updated: 2018-12-30T07:00:00+02:00
tags: node
tags_weight: 50
path: node-environment-variables
---

The `process` core module of Node provides the `env` property which hosts all the environment variables that were set at the moment the process was started.

Here is an example that accesses the NODE_ENV environment variable, which is set to `development` by default.

> Note: `process` does not require a "require", it's automatically available.

```js
process.env.NODE_ENV // "development"
```

Setting it to "production" before the script runs will tell Node that this is a production environment.

In the same way you can access any custom environment variable you set.

Here we set 2 variables for API_KEY and API_SECRET

```bash
API_KEY=123123 API_SECRET=456456 node app.js
```

We can get them in Node.js by running

```js
process.env.API_KEY // "123123"
process.env.API_SECRET // "456456"
```