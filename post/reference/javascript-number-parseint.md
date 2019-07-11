---
title: "The Number parseInt() method"
description: "Find out all about the JavaScript parseInt() method of the Number object"
date: 2019-03-18T07:00:00+02:00
tags: js
---

Parses the argument as an integer number and returns it:

```js
Number.parseInt('10') //10
Number.parseInt('10.00') //10
Number.parseInt('237,21') //237
Number.parseInt('237.21') //237
Number.parseInt('12 34 56') //12
Number.parseInt(' 36 ') //36
Number.parseInt('36 is my age') //36
```

As you can see `Number.parseInt()` is pretty flexible. It can also convert strings with words, extracting the _first_ number, but the string must start with a number:

```js
Number.parseInt('I am Flavio and I am 36') //NaN
```

You can add a second parameter to specify the radix. Radix 10 is default but you can use octal or hexadecimal number conversions too:

```js
Number.parseInt('10', 10) //10
Number.parseInt('010') //10
Number.parseInt('010', 8) //8
Number.parseInt('10', 8) //8
Number.parseInt('10', 16) //16
```
