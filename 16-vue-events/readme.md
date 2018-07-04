## What are Vue.js events

Vue.js allows us to intercept any DOM event by using the `v-on` directive on an element.

If we want to do something when a click event happens in this element:

```html
<template>
  <a>Click me!</a>
</template>
```

we add a `v-on` directive:

```html
<template>
  <a v-on:click="handleClick">Click me!</a>
</template>
```

Vue also offers a very convenient alternative syntax for this:

```html
<template>
  <a @click="handleClick">Click me!</a>
</template>
```

You can choose to use the parentheses or not. `@click="handleClick"` is equivalent to `@click="handleClick()"`.

`handleClick` is a method attached to the component:

```html
<script>
export default {
  methods: {
    handleClick: function(event) {
      console.log(event)
    }
  }
}
</script>
```

What you need to know here is that you can pass parameters from events: `@click="handleClick(param)"` and they will be received inside the method.

## Access the original event object

In many cases, you will want to perform an action on the event object or look up some property in it. How can you access it?

Use the special `$event` directive:

```html
<template>
  <a @click="handleClick($event)">Click me!</a>
</template>

<script>
export default {
  methods: {
    handleClick: function(event) {
      console.log(event)
    }
  }
}
</script>
```

and if you already pass a variable:

```html
<template>
  <a @click="handleClick('something', $event)">Click me!</a>
</template>

<script>
export default {
  methods: {
    handleClick: function(text, event) {
      console.log(text)
      console.log(event)
    }
  }
}
</script>
```

From there you could call `event.preventDefault()`, but there's a better way: event modifiers

## Event modifiers

Instead of messing with DOM "things" in your methods, tell Vue to handle things for you:

- `@click.prevent` call `event.preventDefault()`
- `@click.stop` call `event.stopPropagation()`
- `@click.passive` makes use of the [passive option of addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#Parameters)
- `@click.capture` uses event capturing instead of event bubbling
- `@click.self` make sure the click event was not bubbled from a child event, but directly happened on that element
- `@click.once` the event will only be triggered exactly once

All those options can be combined by appending on modifier after the other.

For more on propagation, bubbling/capturing see my [JavaScript events guide](/javascript-events/).
