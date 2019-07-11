---
title: "The Number parseFloat() method"
description: "Find out all about the JavaScript parseFloat() method of the Number object"
date: 2019-03-17T07:00:00+02:00
tags: js
---

Parses the argument as a float number and returns it. The argument is a string:

```js
Number.parseFloat('10') //10
Number.parseFloat('10.00') //10
Number.parseFloat('237,21') //237
Number.parseFloat('237.21') //237.21
Number.parseFloat('12 34 56') //12
Number.parseFloat(' 36 ') //36
Number.parseFloat('36 is my age') //36

Number.parseFloat('-10') //-10
Number.parseFloat('-10.2') //-10.2
```

As you can see `Number.parseFloat()` is pretty flexible. It can also convert strings with words, extracting the _first_ number, but the string must start with a number:

```js
Number.parseFloat('I am Flavio and I am 36') //NaN
```

It only handles radix 10 numbers.
