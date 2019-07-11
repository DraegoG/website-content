---
title: "Vue, how to use a prop as the class name"
description: "Sometimes you pass a prop to a component, and you want to use that prop value as the class name. How to do that?"
date: 2018-06-23T07:04:59+02:00
tags: vue
---

Say you have a Car component.

You want to add a class to its output based on a prop.

So maybe the prop is called `color`, and you use it like this in other parts of the app:

```html
<Car color="red">
<Car color="blue">
```

In your Car component you first need to declare the color prop:

```html
<script>
export default {
  name: 'Car',
  props: {
    color: String
  }
}
</script>
```

then you can use it in the template part:

```html
<template>
  <div :class="color"></div>
</template>
```

If you want to add a `car` class, plus the class determined by the color prop, you can use this syntax:

```html
<template>
  <div :class="['car', color]"></div>
</template>
```

Happy coding!