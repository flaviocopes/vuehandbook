A watcher is a special Vue.js feature that allows you to spy on one property of the component state, and run a function when that property value changes.

Here's an example. We have a component that shows a name, and allows you to change it by clicking a button:

```html
<template>
  <p>My name is {{name}}</p>
  <button @click="changeName()">Change my name!</button>
</template>

<script>
export default {
  data() {
    return {
      name: 'Flavio'
    }
  },
  methods: {
    changeName: function() {
      this.name = 'Flavius'
    }
  }
}
</script>
```

When the name changes we want to do something, like printing a console log.

We can do so by adding to the `watch` object a property named as the data property we want to watch over:

```html
<script>
export default {
  data() {
    return {
      name: 'Flavio'
    }
  },
  methods: {
    changeName: function() {
      this.name = 'Flavius'
    }
  },
  watch: {
    name: function() {
      console.log(this.name)
    }
  }
}
</script>
```

The function assigned to `watch.name` can optionally accept 2 parameters. The first is the new property value. The second is the old property value:

```html
<script>
export default {
  /* ... */
  watch: {
    name: function(newValue, oldValue) {
      console.log(newValue, oldValue)
    }
  }
}
</script>
```

Watchers cannot be looked up from a template as you can with computed properties.
