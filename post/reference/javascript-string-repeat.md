---
title: "The String repeat() method"
description: "Find out all about the JavaScript repeat() method of a string"
date: 2019-02-27T07:00:00+02:00
tags: js
---

Introduced in [ES2015](/es6/), repeats the strings for the specificed number of times:

```js
'Ho'.repeat(3) //'HoHoHo'
```

Returns an empty string if there is no parameter, or the parameter is `0`. If the parameter is negative you'll get a RangeError.
