---
title: JavaScript Return Values
date: 2019-06-09T07:00:00+02:00
description: "Learn the basics of JavaScript Return Values"
tags: js
---

Every function returns a value, which by default is `undefined`.

![Undefined return value](undefined-return-value.png)

Any function is terminated when its lines of code end, or when the execution flow finds a `return` keyword.

When JavaScript encounters this keyword it exits the function execution and gives control back to its caller.

If you pass a value, that value is returned as the result of the function:

```js
const dosomething = () => {
  return 'test'
}
const result = dosomething() // result === 'test'
```

You can only return one value.

To _simulate_ returning multiple values, you can return an **object literal**, or an **array**, and use a destructuring assignment when calling the function.

Using arrays:

![Destructuring using arrays](destructuring-return-array.png)

Using objects:

![Destructuring using objects](destructuring-return-object.png)
