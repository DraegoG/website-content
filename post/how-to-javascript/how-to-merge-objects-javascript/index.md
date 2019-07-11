---
title: "How to merge two objects in JavaScript"
date: 2018-11-30T07:00:00+02:00
updated: 2019-06-05T07:00:00+02:00
description: "Find out how to merge 2 JavaScript objects and create a new object that combines the properties"
tags: js
---

<div class="rwd-video">
<iframe width="560" height="315" src="https://www.youtube.com/embed/5Lb4wcHupUo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<br>

[ES6](/es6/) in 2015 introduced the [**spread operator**](/javascript-spread-operator/), which is the perfect way to merge two simple objects into one:

```js
const object1 = {
  name: 'Flavio'
}

const object2 = {
  age: 35
}

const object3 = {...object1, ...object2 }
```

If both objects have a property with the same name, then the second object property overwrites the first.

The best solution in this case is to use Lodash and its [`merge()` method](https://www.npmjs.com/package/lodash.merge), which will perform a deeper merge, recursively merging object properties and arrays.

[See the documentation for it on the Lodash docs](https://lodash.com/docs/4.17.11#merge).