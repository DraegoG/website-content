---
title: "Vue, how to use a v-model"
description: "The v-model Vue directive allows us to create a two-way binding. Learn how to use it"
date: 2018-07-13T07:04:59+02:00
tags: vue
---

The `v-model` Vue directive allows us to create a two-way binding.

You can bind a form input element for example, and make it change the Vue data property when the user changes the content of the field:

```html
<input v-model="message" placeholder="Enter a message">
<p>Message is: {{ message }}</p>
```

```html
<select v-model="selected">
  <option disabled value="">Choose a fruit</option>
  <option>Apple</option>
  <option>Banana</option>
  <option>Strawberry</option>
</select>
<span>Fruit chosen: {{ selected }}</span>
```

## Handy directive modifiers

To make the model update when the change event occurs, and not any time the user presses a key, you can use `v-model.lazy` instead of just `v.model`.

Working with input fields, `v-model.trim` is useful because it automatically removes whitespace.

And if you accept a number instead than a string, make sure you use `v-model.number`.

## Nested properties

Say you have a shopping cart, and you have a component that holds a form to add a product:

```html
<template>
  <div class="">
    <h1>Add Product</h1>
    <label>Name</label>: <input>
    <label>Description</label>: <textarea></textarea>
    <button @click="addProduct">Add</button>
  </div>
</template>

<script>
export default {
  name: 'AddProduct',
  data() {
    return {
      product: {
        name: '',
        description: ''
      }
    }
  },
  methods: {
    addProduct() {
      console.log(this.product)
    }
  }
}
</script>
```

To make the form update the inner properties of the `product` state value, you use `product.*`:

```html
<label>Name</label>: <input v-model="product.name">
<label>Description</label>: <textarea v-model="product.description"></textarea>
```
