---
title: "Generate random and unique strings in JavaScript"
description: "How I created an array of 5000 unique strings in JavaScript"
date: 2018-07-21T07:06:29+02:00
tags: js
tags_weight: 40
---

As I was building the platform for my online course I had the problem of generating a few thousands unique URLs.

Every person taking the course will be assigned a unique URL. The backend knows about all those URLs and maps a valid URL to the course content.

I wanted a unique URL because I can associate a URL to a purchase email.

In this way, I can avoid having a login, and at the same time having a separate URL for each person lets me block eventual abuse if that URL gets unintentionally or intentionally shared in the public.

So I set out to write my Node.js script.

I used the [randomstring](https://www.npmjs.com/package/randomstring) package, and I added numbers to a [Set object](/javascript-data-structures-set/) until I got the number I wanted. Using a Set means every string will be unique because calling `add` and passing a duplicate string will silently do nothing.

I made a `generateStrings()` function that returns the set:

```js
const generateStrings = (numberOfStrings, stringLength) => {
  const randomstring = require('randomstring')
  const s = new Set()

  while (s.size < numberOfStrings) {
    s.add(randomstring.generate(stringLength))
  }

  return s
}
```

I can call it using

```js
const strings = generateStrings(100, 20)
```

where 100 is the number of strings I want, and 20 is the length of each string.

Once we get the set, we can iterate over them using the `values()` Set method:

```js
for (const value of strings.values()) {
  console.log(value)
}
```