---
title: How to determine if a date is today in JavaScript
description: "Discover how to find out if a Date object represents a today datetime"
date: 2018-10-13T07:00:00+02:00
tags: node
---

How can you determine if a JavaScript Date object instance is a representation of a date/time that is "today"?

Given a Date instance, we can use the `getDate()`, `getMonth()` and `getFullYear()` methods, which return the day, month and year of a date, and compare them to today, which can be retrieved using `new Date()`.

Here's a small function that does exactly that, returning true if the argument is today.

```js
const isToday = (someDate) => {
  const today = new Date()
  return someDate.getDate() == today.getDate() &&
    someDate.getMonth() == today.getMonth() &&
    someDate.getFullYear() == today.getFullYear()
}
```

You can use it like this:

```js
const today = isToday(myDate)
```

Check out the [JavaScript Date guide](/javascript-dates/) to find out more how to handle the Date object, if you need.
