---
title: A Moment.js tutorial
date: 2018-07-08T07:04:59+02:00
description: "Moment.js is a great help in managing dates in JavaScript"
tags: js
tags_weight: 45
---

[Moment.js](https://momentjs.com) is an awesome JavaScript library that helps you manage dates, in the browser and in Node.js as well.

This article aims to explain the basics and the most common usages of this library.

## Installation

You can include it directly in your page using a script tag, from unpkg.com:

```html
<script src="https://unpkg.com/moment" />
```

or using [npm](/npm/):

```bash
npm install moment
```

If you install using npm you need to import the package (using [ES Modules](/es-modules/)):

```js
import moment from 'moment'
```

or require it (using [CommonJS](/commonjs/)):

```js
const moment = require('moment')
```

## Get the current date and time

```js
const date = moment()
```

## Parse a date

A moment object can be initialized with a date by passing it a string:

```js
const date = moment(string)
```

it accepts any string, parsed according to (in order):

- [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)
- [The RFC 2822 Date Time format](https://tools.ietf.org/html/rfc2822#section-3.3)
- the formats accepted by the Date object

ISO 8601 is definitely the most convenient. Here's a format reference:

Format | Meaning | Example
---------|----------| ---
 YYYY | 4-digits Year | 2018
 YY | 2-digits Year | 18
 M | 2-digits Month number, omits leading 0 | 7
 MM | 2-digits Month number | 07
 MMM | 3-letters Month name | Jul
 MMMM | Full Month name | July
 dddd | Full day name | Sunday
 gggg | 4-digits Week year | 2018
 gg | 2-digits Week year | 18
 w | Week of the year without leading zero | 18
 ww | Week of the year with leading zero | 18
 e | Day of the week, starts at 0 | 4
 D | 2-digits day number, omits leading 0 | 9
 DD | 2-digits day number | 09
 Do | Day number with ordinal | 9th
 T | Indicates the start of the time part |
 HH | 2-digits hours (24 hour time) from 0 to 23 | 22
 H | 2-digits hours (24 hour time) from 0 to 23 without leading 0 | 22
 kk | 2-digits hours (24 hour time) from 1 to 24| 23
 k | 2-digits hours (24 hour time) from 1 to 24 without leading 0 | 23
 a/A | `am` or `pm` | pm
 hh | 2-digits hours (12 hour time) | 11
 mm | 2-digits minutes | 22
 ss | 2-digits seconds |40
 s | 2-digits seconds without leading zero |40
 S | 1-digits milliseconds | 1
 SS | 2-digits milliseconds | 12
 SSS | 3-digits milliseconds | 123
 Z | The timezone | +02:00
 x | UNIX timestamp in milliseconds | 1410432140575

## Set a date

## Format a date

When you want to output the content of a plain JavaScript Date object, you have little options to determine the formatting. All you can do is to use the built-in methods, and compose the date as you want using them.

Moment offers a handy way to format the date according to your needs, using the `format()` method:

```js
date.format(string)
```

The string format accepts the same formats I described in the "Parse a date" section above.

Example:

```js
moment().format("YYYY Do MM")
```

Moment provides some constants you can use instead of writing your own format:

Constant | Format | Example
---------|----------| ---
`moment.HTML5_FMT.DATETIME_LOCAL` | 	YYYY-MM-DDTHH:mm |	2017-12-14T16:34
`moment.HTML5_FMT.DATETIME_LOCAL_SECONDS` | 	YYYY-MM-DDTHH:mm:ss |	2017-12-14T16:34:10
`moment.HTML5_FMT.DATETIME_LOCAL_MS` | 	YYYY-MM-DDTHH:mm:ss.SSS |	2017-12-14T16:34:10.234
`moment.HTML5_FMT.DATE` | 	YYYY-MM-DD |	2017-12-14
`moment.HTML5_FMT.TIME` | 	HH:mm |	16:34
`moment.HTML5_FMT.TIME_SECONDS` | 	HH:mm:ss |	16:34:10
`moment.HTML5_FMT.TIME_MS` | 	HH:mm:ss.SSS |	16:34:10.234
`moment.HTML5_FMT.WEEK` | 	YYYY-[W]WW |	2017-W50
`moment.HTML5_FMT.MONTH` | 	YYYY-MM	 |2017-12

## Validating a date

Any date can be checked for validity using the `isValid()` method:

```js
moment('2018-13-23').isValid() //false
moment('2018-11-23').isValid() //true
```

## Time ago, time until date

Use `fromNow()`. Strings are localized:

```js
moment('2016-11-23').fromNow() //2 years ago
moment('2018-05-23').fromNow() //a month ago
moment('2018-11-23').fromNow() //in 5 months
```

if you pass `true` to fromNow(), it just shows the difference, without reference to future/past.

```js
moment('2016-11-23').fromNow(true) //2 years
moment('2018-05-23').fromNow(true) //a month
moment('2018-11-23').fromNow(true) //5 months
```

## Manipulate a date

You can add or subtract any amount of time to a date:

```js
moment('2016-11-23').add(1, 'years')
moment('2016-11-23').subtract(1, 'years')
```

You can use those values:

- `years`
- `quarters`
- `months`
- `weeks`
- `days`
- `hours`
- `minutes`
- `seconds`
- `milliseconds`
