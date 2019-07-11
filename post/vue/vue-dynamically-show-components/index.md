---
title: Dynamically show a Vue component
date: 2018-07-04T07:07:09+02:00
description: "Using Vue you define the application layout using components. In the beginning you manually place components where you want, but at some point you need to have a more flexible way to show or hide components based on the application state"
tags: vue
---

## Using conditional directives

The simplest option is to use the `v-if` and `v-else` directives.

Here's an example. The `v-if` directive checks the `noTodos` computed property, which returns false if the state property `todos` contains at least one item:

```html
<template>
  <main>
    <AddFirstTodo v-if="noTodos" />
    <div v-else>
      <AddTodo />
      <Todos :todos=todos />
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
    }
  },
  computed: {
    noTodos() {
      return this.todos.length === 0
    }
  }
}
</script>
```

This allows to solve the needs of many applications without reaching for more complex setups. Conditionals can be nested, too, like this:

```html
<template>
  <main>
    <Component1 v-if="shouldShowComponent1" />
    <div v-else>
      <Component2 v-if="shouldShowComponent2" />
      <div v-else>
        <Component3 />
      </div>
    </div>
  </main>
</template>
```

## Using the `component` Component and `is`

Instead of creating `v-if` and `v-else` structures, you can build your template so that there's a placeholder that will be dynamically assigned a component.

That's what the `component` component does, with the help of the `v-bind:is` directive.

```html
<component v-bind:is="componentName"></component>
```

`componentName` is a property of the state that identifies the name of the component that we want to render. It can be part of the state, or a computed property:

```html
<script>
export default {
  data() {
    return {
      componentName: 'aComponent',
    }
  }
}
</script>
```
