Vue.js uses a templating language that's a superset of HTML.

Any HTML is a valid Vue.js template, and in addition to that, Vue.js provides two powerful things: **interpolation** and **directives**.

I'm going to detail interpolation in this article, and make a new one tomorrow for directives.

This is a valid Vue.js template:

```html
<span>Hello!</span>
```

This template can be put inside a Vue component declared explicitly:

```js
new Vue({
  template: '<span>Hello!</span>'
})
```

or it can be put into a Single File Component:

```html
<template>
  <span>Hello!</span>
</template>
```

This first example is very basic. The next step is making it output a piece of the component state, for example, a name.

This can be done using interpolation. First, we add some data to our component:

```js
new Vue({
  data: {
    name: 'Flavio'
  },
  template: '<span>Hello!</span>'
})
```

and then we can add it to our template using the double brackets syntax:

```js
new Vue({
  data: {
    name: 'Flavio'
  },
  template: '<span>Hello {{name}}!</span>'
})
```

One interesting thing here. See how we just used `name` instead of `this.data.name`?

This is because Vue.js does some internal binding and lets the template use the property as if it was local. Pretty handy.

In a single file component, that would be:

```html
<template>
  <span>Hello {{name}}!</span>
</template>

<script>
export default {
  data() {
    return {
      name: 'Flavio'
    }
  }
}
</script>
```

I used a regular function in my export. Why not an arrow function?

This is because in `data` we might need to access a method in our component instance, and we can't do that if `this` is not bound to the component, so arrow functions usage is not possible.

We could use an arrow function, but then I would need to remember to switch to a regular function in case I use `this`. Better play it safe, I think.

Now, back to the interpolation.

`{{ name }}` reminds of Mustache / Handlebars template interpolation, but it's just a visual reminder.

While in those templating engines they are "dumb", in Vue, you can do much more, it's more flexible.

You can use **any JavaScript expression** inside your interpolations, but you're limited to just one expression:

```js
{
  {
    name.reverse()
  }
}
```

```js
{
  {
    name === 'Flavio' ? 'Flavio' : 'stranger'
  }
}
```

Vue provides access to some global objects inside templates, including Math and Date, so you can use them:

```js
{
  {
    Math.sqrt(16) * Math.random()
  }
}
```

It's best to avoid adding complex logic to templates, but the fact Vue allows it gives us more flexibility, especially when trying things out.

We can first try to put an expression in the template, and then move it to a computed property or method later on.

The value included in any interpolation will be updated upon a change of any of the data properties it relies on.

You can avoid this reactivity by using the `v-once` directive.

The result is always escaped, so you can't have HTML in the output.

If you need to have an HTML snippet you need to use the `v-html` directive instead.
