---
title: The JavaScript delete Operator
date: 2019-06-05T07:00:00+02:00
description: "Learn the basics of the JavaScript delete Operator"
tags: js
---

The `delete` JavaScript operator is used to delete a property from an object.

Say you have this object:

```js
const car = {
  model: 'Fiesta',
  color: 'green'
}
```

You can delete any property from it, or method, using the `delete` operator:

```js
delete car.model
```

You can also reference the property/method using the brackets syntax:

```js
delete car['color']
```
