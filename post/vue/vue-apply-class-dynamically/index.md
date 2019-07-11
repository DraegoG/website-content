---
title: How to dynamically apply a class using Vue
description: "Learn how to make Vue output a class or another depending on some condition"
date: 2018-07-12T07:04:59+02:00
tags: vue
---

Say you want to apply the class `background-dark` to an element, if the `isDark` prop is true, and otherwise add the `background-light`.

How would you do that in Vue?

Use `:class="[ isDark ? 'background-dark' : 'background-light' ]"`

Here's an example:

```html
<template>
  <div :class="[ isDark ? 'background-dark' : 'background-light' ]">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    isDark: Boolean
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .background-dark {
    background-color: #000;
  }
  .background-light {
    background-color: #fff;
  }
</style>
```

(many thanks to [Adam Wathan](https://twitter.com/adamwathan) for suggesting this to me on the Tailwind Slack)