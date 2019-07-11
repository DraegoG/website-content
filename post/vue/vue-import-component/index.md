---
title: "Vue, use a component inside another component"
description: "Here's how to import a component inside another component in Vue.js"
date: 2018-06-22T07:04:59+02:00
tags: vue
---

Say you have a Pixel component in `src/components/Pixel.vue`

In another component, Canvas, which is located in `src/components/Canvas.vue`, you can import that Pixel component by importing it inside the `script` tag of the Vue Single File Component:

```html
<template>
  <p>Canvas</p>
  <Pixel />
</template>

<script>
import Pixel from './Pixel'

export default {
  name: 'App',
  components: {
    Pixel
  }
}
</script>
```