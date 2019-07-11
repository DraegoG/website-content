---
title: JavaScript Type Conversions (casting)
date: 2019-05-30T07:00:00+02:00
description: "Learn the basics of JavaScript Type Conversions"
tags: js
---

Even if JavaScript is a loosely typed language, you might have the need to convert a value from a type to another.

In JavaScript  we have those primitive types:

- [`Number`](/javascript-number/)
- [`String`](/javascript-string/)
- `Boolean`
- `Symbol`

and the object type:

- [`Object`](/javascript-object/)

(plus `null` and `undefined`, but there's no point in casting from/to them)

For example, you might want to convert:

- a number to a string
- a string to a number
- a string to a boolean
- a boolean to a string

...and so on.

Here are the techniques you can use to convert from one type to another. I cover the most common cases.

## Converting to strings

In general converting from anything to a string is usually a matter of calling the `toString()` method on any value, and JavaScript will create a string value corresponding to that type. Or you can pass any value to the `String()` global function.

### Casting from number to string

Use the String global function, or the Number type `toString()` method:

```js
String(10) //"10"
(10).toString() //"10"
```

### Casting from boolean to string

Use the String global function, or the Boolean type `toString()` method:

```js
String(true) //"true"
true.toString() //"true"
String(false) //"false"
false.toString() //"false"
```

### Casting from date to string

Use the String global function, or the Date type `toString()` method:

```js
String(new Date('2019-01-22'))
//"Tue Jan 22 2019 01:00:00 GMT+0100 (Central European Standard Time)"

(new Date('2019-01-22')).toString()
//"Tue Jan 22 2019 01:00:00 GMT+0100 (Central European Standard Time)"
```

### Special cases with string

```js
String(null) //"null"
String(undefined) //"undefined"
String(NaN) //"NaN"
```

## Converting to numbers

### Casting from string to number

We can do this by using the `Number()` global function, which is sort of a constructor. We can pass it a string, and JavaScript will figure out how to convert it to a number:

```js
Number("1") //1
Number("0") //0
```

Strings are trimmed before being converted to numbers:

```js
Number(" 1 ") //1
```

passing an empty string defaults to 0:

```js
Number("") //0
```

and to have work with decimals you use a dot:

```js
Number("12.2")
```

If a string contains invalid characters, it will generate a `NaN`.

This are the basics of converting to numbers, but I give a lot more details in [how to convert a string to a number in JavaScript](/how-to-convert-string-to-number-javascript/). There are other ways to generate numbers from string including `parseInt()`, `parseFloat()`, `Math.floor()`, the unary `+` operator.

### Casting from boolean to number

Just as we did for string, passing a boolean to `Number()` will return either 0 or 1:

```js
Number(true) //1
Number(false) //0
```

### Casting from date to number

If you pass a Date object to `Number()`, it will return the date timestamp, which is the best date to number conversion you can get.

### Special cases with number

```js
Number(null) //0
Number(undefined) //NaN
Number(NaN) //NaN
```

## Converting to booleans

Any value can be converted to boolean passing it to  `Boolean()`.

All values will resolve to `true` except:

```js
Boolean(false) //false
Boolean(0) //false
Boolean(NaN) //false
Boolean("") //false
Boolean(null) //false
Boolean(undefined) //false
```
