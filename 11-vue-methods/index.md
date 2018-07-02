## What are Vue.js methods

A Vue method is a function associated with the Vue instance.

Methods are defined inside the `methods` property:

```js
new Vue({
  methods: {
    handleClick: function() {
      alert('test')
    }
  }
})
```

or in the case of Single File Components:

```html
<script>
export default {
  methods: {
    handleClick: function() {
      alert('test')
    }
  }
}
</script>
```

Methods are especially useful when you need to perform an action and you attach a `v-on` directive on an element to handle **events**. Like this one, which calls `handleClick` when the element is clicked:

```html
<template>
  <a @click="handleClick">Click me!</a>
</template>
```

## Pass parameters to Vue.js methods

Methods can accept parameters.

In this case, you just pass the parameter in the template, and you

```html
<template>
  <a @click="handleClick('something')">Click me!</a>
</template>
```

```js
new Vue({
  methods: {
    handleClick: function(text) {
      alert(text)
    }
  }
})
```

or in the case of Single File Components:

```html
<script>
export default {
  methods: {
    handleClick: function(text) {
      alert(text)
    }
  }
}
</script>
```

## How to access data from a method

You can access any of the data properties of the Vue component by using `this.propertyName`:

```html
<template>
  <a @click="handleClick()">Click me!</a>
</template>

<script>
export default {
  data() {
    return {
      name: 'Flavio'
    }
  },
  methods: {
    handleClick: function() {
      console.log(this.name)
    }
  }
}
</script>
```

We don't have to use `this.data.name`, just `this.name`. Vue does provide a transparent binding for us. Using `this.data.name` will raise an error.

Methods are closely interlinked to events.
