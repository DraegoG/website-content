---
title: "Vue.js Computed Properties"
seotitle: "Vue.js Computed Properties Tutorial"
description: "Learn how you can use Vue Computed Properties to cache calculations"
date: 2018-06-07T07:04:59+02:00
tags: vue
---

<!-- TOC -->

- [What is a Computed Property](#what-is-a-computed property)
- [An example of a computed property](#an-example-of-a-computed-property)
- [Computed properties vs methods](#computed-properties-vs-methods)

<!-- /TOC -->

---

## What is a Computed Property

In Vue.js you can output any data value using parentheses:

```html
<template>
  <p>{{ count }}</p>
</template>

<script>
export default {
  data() {
    return {
      count: 1
    }
  }
}
</script>
```

This property can host some small computations, for example

```html
<template>
  {{ count * 10 }}
</template>
```

but you're limited to a single JavaScript _expression_.

In addition to this technical limitation, you also need to consider that templates should only be concerned with displaying data to the user, not perform logic computations.

To do something more a single expression, and to have more declarative templates, that you use a **computed property**.

Computed properties are defined in the `computed` property of the Vue component:

```html
<script>
export default {
  computed: {

  }
}
</script>
```

## An example of a computed property

Here's an example code that uses a computed property `count` to calculate the output. Notice:

1.  I didn't have to call `count()`. Vue.js automatically invokes the function
2.  I used a regular function (not an arrow function) to define the `count` computed property because I need to be able to access the component instance through `this`.

```html
<template>
  <p>{{ count }}</p>
</template>

<script>
export default {
  data() {
    return {
      items: [1, 2, 3]
    }
  },
  computed: {
    count: function() {
      return 'The count is ' + this.items.length * 10
    }
  }
}
</script>
```

## Computed properties vs methods

If you already know [Vue methods](/vue-methods/), you may wonder what's the difference.

First, methods must be called, not just referenced, so you'd need to do call `count()` instead of `count` if you have a `count` method:

```html
<script>
export default {
  data() {
    return {
      items: [1, 2, 3]
    }
  },
  methods: {
    count: function() {
      return 'The count is ' + this.items.length * 10
    }
  }
}
</script>
```

But the main difference is that **computed properties are cached**.

The result of the `count` computed property is internally cached until the `items` data property changes.

Important: computed properties are **only updated when a reactive source updates**. Regular JavaScript methods are not reactive, so a common example is to use `Date.now()`:

```html
<template>
  <p>{{ now }}</p>
</template>

<script>
export default {
  computed: {
    now: function () {
      return Date.now()
    }
  }
}
</script>
```

It will render once, and then it will not be updated even when the component re-renders. Just on a page refresh, when the Vue component is quit and reinitialized.

In this case a method is better suited for your needs.
