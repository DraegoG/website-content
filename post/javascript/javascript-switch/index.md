---
title: The JavaScript Switch Conditional
date: 2019-06-03T07:00:00+02:00
description: "Learn the basics of the JavaScript Switch Conditional"
tags: js
---

An `if/else` statement is great when you have a few options to choose.

When they are too many however it might be overkill. Your code will look too complex.

In this case you might want to use a `switch` conditional:

```js
switch(<expression>) {
  //cases
}
```

based on the result of the expression, JavaScript will trigger one specific case you define:

```js
const a = 2
switch(a) {
  case 1:
    //handle case a is 1
    break
  case 2:
    //handle case a is 2
    break
  case 3:
    //handle case a is 3
    break
}
```

You must add a `break` statement at the bottom of each case, otherwise JavaScript will also execute the code in the next case (and sometimes this is useful, but beware of bugs).
When used inside a function, if the switch defines a return value, instead of using `break` you can just use `return`:


```js
const doSomething = (a) => {
  switch(a) {
    case 1:
      //handle case a is 1
      return 'handled 1'
    case 2:
      //handle case a is 2
      return 'handled 2'
    case 3:
      //handle case a is 3
      return 'handled 3'
  }
}
```

You can provide a `default` special case, which is called when no case handles the result of the expression:

```js
const a = 2
switch(a) {
  case 1:
    //handle case a is 1
    break
  case 2:
    //handle case a is 2
    break
  case 3:
    //handle case a is 3
    break
  default:
    //handle all other cases
    break
}
```
