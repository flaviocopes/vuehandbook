We saw in Vue.js templates and interpolations how you can embed data in Vue templates.

This article explains the other technique offered by Vue.js in templates: **directives**.

Directives, are basically like HTML attributes which are added inside templates. They all start with `v-`, to indicate that's a Vue special attribute.

Let's see each of the Vue directives in details.

## `v-text`

Instead of using interpolation, you can use the `v-text` directive. It performs the same job:

```html
<span v-text="name"></span>
```

## `v-once`

You know how `{{ name }}` binds to the `name` property of the component data.

Any time `name` changes in your component data, Vue is going to update the value represented in the browser.

Unless you use the `v-once` directive, which is basically like an HTML attribute:

```html
<span v-once>{{ name }}</span>
```

## `v-html`

When you use interpolation to print a data property, the HTML is escaped. This is a great way that Vue uses to automatically protect from XSS attacks.

There are cases however where you want to output HTML and make the browser interpret it. You can use the `v-html` directive:

```html
<span v-html="someHtml"></span>
```

## `v-bind`

Interpolation only works in the tag content. You can't use it on attributes.

Attributes must use `v-bind`:

```html
<a v-bind:href="url">{{ linkText }}</a>
```

`v-bind` is so common that there is a shorthand syntax for it:

```html
<a v-bind:href="url">{{ linkText }}</a>
<a :href="url">{{ linkText }}</a>
```

## Two-way binding using `v-model`

`v-model` lets us bind a form input element for example, and make it change the Vue data property when the user changes the content of the field:

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

## Using expressions

You can use any JavaScript expression inside a directive:

```html
<span v-text="'Hi, ' + name + '!'"></span>
```

```html
<a v-bind:href="'https://' + domain + path">{{ linkText }}</a>
```

Any variable used in a directive references the corresponding data property.

## Conditionals

Inside a directive you can use the ternary operator to perform a conditional check, since that's an expression:

```html
<span v-text="name == Flavio ? 'Hi Flavio!' : 'Hi' + name + '!'"></span>
```

There are dedicated directives that allow you to perform more organized conditionals: `v-if`, `v-else` and `v-else-if`.

```html
<p v-if="shouldShowThis">Hey!</p>
```

`shouldShowThis` is a boolean value contained in the component's data.

## Loops

`v-for` allows you to render a list of items. Use it in combination with `v-bind` to set the properties of each item in the list.

You can iterate on a simple array of values:

```html
<template>
  <ul>
    <li v-for="item in items">{{ item }}</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      items: ['car', 'bike', 'dog']
    }
  }
}
</script>
```

Or on an array of objects:

```html
<template>
  <div>
    <!-- using interpolation -->
    <ul>
      <li v-for="todo in todos">{{ todo.title }}</li>
    </ul>
    <!-- using v-text -->
    <ul>
      <li v-for="todo in todos" v-text="todo.title"></li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { id: 1, title: 'Do something' },
        { id: 2, title: 'Do something else' }
      ]
    }
  }
}
</script>
```

`v-for` can give you the index using:

```html
<li v-for="(todo, index) in todos"></li>
```

## Events

`v-on` allows you to listen to DOM events, and trigger a method when the event happens. Here we listen for a click event:

```html
<template>
  <a v-on:click="handleClick">Click me!</a>
</template>

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

You can pass parameters to any event:

```html
<template>
  <a v-on:click="handleClick('test')">Click me!</a>
</template>

<script>
export default {
  methods: {
    handleClick: function(value) {
      alert(value)
    }
  }
}
</script>
```

and small bits of JavaScript (a single expression) can be put directly into the template:

```html
<template>
  <a v-on:click="counter = counter + 1">{{counter}}</a>
</template>

<script>
export default {
  data: function() {
    return {
      counter: 0
    }
  }
}
</script>
```

`click` is just one kind of event. A common event is `submit`, which you can bind using `v-on:submit`.

`v-on` is so common that there is a shorthand syntax for it, `@`:

```html
<a v-on:click="handleClick">Click me!</a>
<a @:click="handleClick">Click me!</a>
```

> More details on v-on in the Events section

## Show or hide

You can choose to only show an element in the DOM if a particular property of the Vue instance evaluates to true, using `v-show`:

```html
<p v-show="isTrue">Something</p>
```

The element is still inserted in the DOM, but set to `display: none` if the condition is not satisfied.

## Event directive modifiers

Vue offers some optional event modifiers you can use in association with `v-on`, which automatically make the event do something without you explicitly coding it in your event handler.

One good example is `.prevent`, which automatically calls `preventDefault()` on the event.

In this case, the form does not cause the page to be reloaded, which is the default behavior:

```html
<form v-on:submit.prevent="formSubmitted"></form>
```

Other modifiers include `.stop`, `.capture`, `.self`, `.once`, `.passive` and they are [described in details in the official docs](https://vuejs.org/v2/guide/events.html#Event-Modifiers).

## Custom directives

The Vue default directives already let you do a lot of work, but you can always add new, custom directives if you want.

Read <https://vuejs.org/v2/guide/custom-directive.html> if you're interested in learning more.
