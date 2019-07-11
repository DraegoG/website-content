---
title: "Vue.js Slots"
seotitle: "Vue.js Slots Tutorial"
description: "Slots help you position content in a component, and allow parent components to arrange it."
date: 2018-06-15T07:04:59+02:00
updated: 2019-04-02T18:04:59+02:00
tags: vue
---

A component can be 100% responsible for generating its output, like in this case:

```js
Vue.component('user-name', {
  props: ['name'],
  template: '<p>Hi {{ name }}</p>'
})
```

or it can also let the parent component inject any kind of content into it, using **slots**.

What is a slot? It's a space in your component output that is reserved, waiting to be filled.

You define a slot by putting `<slot></slot>` in a component template:

```js
Vue.component('user-information', {
  template: '<div class="user-information"><slot></slot></div>'
})
```

When using this component, any content added between the opening and closing tag will be added inside the slot placeholder:

```html
<user-information>
  <h2>Hi!</h2>
  <user-name name="Flavio"></user-name>
</user-information>
```

If you put any content side the `<slot></slot>` tags, that serves as the default content in case nothing is passed in.

A complicated component layout might require a better way to organize content, with multiple slots as well.

This is why Vue offers us **named slots**.

## Named slots

With a named slot you can assign parts of a slot to a specific position in your component template layout, and you use a `slot` attribute to any tag, to assign content to that slot.

Anything outside any template tag is added to the main `slot`.

For convenience I use a `page` single file component in this example:

```html
<template>
  <div>
    <main>
      <slot></slot>
    </main>
    <aside>
      <slot name="sidebar"></slot>
    </aside>
  </div>
</template>
```

Here is how we can use it, providing the slots content, in a parent component:

```html
<page>
  <template v-slot:sidebar>
    <ul>
      <li>Home</li>
      <li>Contact</li>
    </ul>
  </template>

  <h2>Page title</h2>
  <p>Page content</p>
</page>
```

There is a handy shorthand, `#`:

```html
<page>
  <template #sidebar>
    <ul>
      <li>Home</li>
      <li>Contact</li>
    </ul>
  </template>

  <h2>Page title</h2>
  <p>Page content</p>
</page>
```

> Note: Vue 2.6 deprecated the `slot` attribute in favor of `v-slot`, and requires it to be added to a `template` tag (while `slot` could be applied to any tag)

## Scoped slots

In a slot, we can't access the data contained in the child component from the parent.

Vue recognizes this use case and provides us a way to do so:

```html
<template>
  <div>
    <main>
      <slot v-bind:dogName="dogName"></slot>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Page',
  data: function() {
    return {
      dogName: 'Roger'
    }
  }
}
</script>
```

In the parent we can access the dog name we passed using:

```html
<page>
  <template v-slot="slotProps">
    {{ slotProps.dogName }}
  </template>
</page>
```

`slotProps` is just a variable we used to access the props we passed. You can also avoid setting a variable just to hold the props you pass to the child component, by destructuring the object on the fly:

```html
<page>
  <template v-slot="{ dogName }">
    {{ dogName }}
  </template>
</page>
```