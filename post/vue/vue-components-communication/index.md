---
title: "Vue.js Components Communication"
booktitle: "Communication among components"
description: "How you can make components communicate in a Vue.js application."
date: 2018-06-20T07:04:59+02:00
tags: vue
---

<!-- TOC -->

- [Props](#props)
- [Events to communicate from children to parent](#events-to-communicate-from-children-to-parent)
- [Using an Event Bus to communicate between any component](#using-an-event-bus-to-communicate-between-any-component)
- [Alternatives](#alternatives)

<!-- /TOC -->

---

Components in Vue can communicate in various ways.

## Props

The first way is using [props](/vue-props/).

Parents "pass down" data by adding arguments to the component declaration:

```html
<template>
  <div>
    <Car color="green" />
  </div>
</template>

<script>
import Car from './components/Car'

export default {
  name: 'App',
  components: {
    Car
  }
}
</script>
```

Props are one-way: from parent to child. Any time the parent changes the prop, the new value is sent to the child and rerendered.

The reverse is not true, and you should never mutate a prop inside the child component.

## Using Events to communicate from children to parent

Events allow you to communicate from the children up to the parent:

```html
<script>
export default {
  name: 'Car',
  methods: {
    handleClick: function() {
      this.$emit('clickedSomething')
    }
  }
}
</script>
```

The parent can intercept this using the `v-on` directive when including the component in its template:

```html
<template>
  <div>
    <Car v-on:clickedSomething="handleClickInParent" />
    <!-- or -->
    <Car @clickedSomething="handleClickInParent" />
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    handleClickInParent: function() {
      //...
    }
  }
}
</script>
```

You can pass parameters of course:

```html
<script>
export default {
  name: 'Car',
  methods: {
    handleClick: function() {
      this.$emit('clickedSomething', param1, param2)
    }
  }
}
</script>
```

and retrieve them from the parent:

```html
<template>
  <div>
    <Car v-on:clickedSomething="handleClickInParent" />
    <!-- or -->
    <Car @clickedSomething="handleClickInParent" />
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    handleClickInParent: function(param1, param2) {
      //...
    }
  }
}
</script>
```

## Using an Event Bus to communicate between any component

Using events you're not limited to child-parent relationships.

You can use the so-called **Event Bus**.

Above we used `this.$emit` to emit an event on the component instance.

What we can do instead is to emit the event on a more generally accessible component.

`this.$root`, the root component, is commonly used for this.

You can also create a Vue component dedicated to this job, and import it where you need.


```html
<script>
export default {
  name: 'Car',
  methods: {
    handleClick: function() {
      this.$root.$emit('clickedSomething')
    }
  }
}
</script>
```

Any other component can listen for this event. You can do so in the `mounted` callback:

```html
<script>
export default {
  name: 'App',
  mounted() {
    this.$root.$on('clickedSomething', () => {
      //...
    })
  }
}
</script>
```

## Alternatives

This is what Vue provides out of the box.

When you outgrow this, you can look into [Vuex](/vuex/) or other 3rd party libraries.