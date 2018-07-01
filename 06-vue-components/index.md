Components are single, independent units of an interface. They can have their own state, markup and style.

## How to use components

Vue components can be defined in 4 main ways.

Let's talk in code.

The first is:

```js
new Vue({
  /* options */
})
```

The second is:

```js
Vue.component('component-name', {
  /* options */
})
```

The third is by using local components: components that only accessible by a specific component, and not available elsewhere (great for encapsulation).

The fourth is in `.vue` files, also called **Single File Components**.

Let's dive into the first 3 ways in details.

Using `new Vue()` or `Vue.component()` is the standard way to use Vue when you're building an application that is not a Single Page Application (SPA), but rather uses Vue.js just in some pages, like in a contact form or in the shopping cart. Or maybe Vue is used in all pages, but the server is rendering the layout, and you serve the HTML to the client, which then loads the Vue application you build.

In a SPA, where it's Vue that builds the HTML, it's more common to use Single File Components as they are more convenient.

You instantiate Vue by mounting it on a DOM element. If you have a `<div id="app"></div>` tag, you will use:

```js
new Vue({ el: '#app' })
```

A component initialized with `new Vue` has no corresponding tag name, so it's usually the main container component.

Other components used in the application are initialized using `Vue.component()`. Such a component allows you to define a tag, with which you can embed the component multiple times in the application, and specify the output of the component in the `template` property:

```html
<div id="app">
  <user-name name="Flavio"></user-name>
</div>
```

```js
Vue.component('user-name', {
  props: ['name'],
  template: '<p>Hi {{ name }}</p>'
})

new Vue({
  el: '#app'
})
```

<div class="web-only">
<hr>

<script async src="//jsfiddle.net/flaviocopes/nvgedhq4/embed/js,html,result/"></script>

<hr>
</div>

What are we doing? We are initializing a Vue root component on `#app`, and inside that we use the Vue component `user-name`, which abstracts our greeting to the user.

The component accepts a prop, which is an attribute we use to pass data down to child components.

In the `Vue.component()` call we passed `user-name` as the first parameter. This gives the component a name. You can write the name in 2 ways here. The first is the one we used, called **kebab-case**. The second is called **PascalCase**, which is like camelCase, but with the first letter capitalized:

```js
Vue.component('UserName', {
  /* ... */
})
```

Vue internally automatically creates an alias from `user-name` to `UserName`, and vice versa, so you can use whatever you like. It's generally best to use `UserName` in the JavaScript, and `user-name` in the template.

## Local components

Any component created using `Vue.component()` is **globally registered**. You don't need to assign it to a variable or pass it around to reuse it in your templates.

You can encapsulate components locally by assigning an object that defines the component object to a variable:

```js
const Sidebar = {
  template: '<aside>Sidebar</aside>'
}
```

and then make it available inside another component by using the `components` property:

```js
new Vue({
  el: '#app',
  components: {
    Sidebar
  }
})
```

You can write the component in the same file, but a great way to do this is to use JavaScript modules:

```js
import Sidebar from './Sidebar'

export default {
  el: '#app',
  components: {
    Sidebar
  }
}
```

## Reusing a component

A child component can be added multiple times. Each separate instance is independent from the others:

```html
<div id="app">
  <user-name name="Flavio"></user-name>
  <user-name name="Roger"></user-name>
  <user-name name="Syd"></user-name>
</div>
```

```js
Vue.component('user-name', {
  props: ['name'],
  template: '<p>Hi {{ name }}</p>'
})

new Vue({
  el: '#app'
})
```

<div class="web-only">
<hr>

<script async src="//jsfiddle.net/flaviocopes/3kebv908/embed/js,html,result/"></script>

<hr>
</div>

## The building blocks of a component

So far we've seen how a component can accept the `el`, `props` and `template` properties.

- `el` is only used in root components initialized using `new Vue({})`, and identifies the DOM element the component will mount on.
- `props` lists all the properties that we can pass down to a child component
- `template` is where we can set up the component template, which will be responsible for defining the output the component generates.

A component accepts other properties:

- `data` the component local state
- `methods`: the component methods
- `computed`: the computed properties associated with the component
- `watch`: the component watchers
