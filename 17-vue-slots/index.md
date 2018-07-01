A component can choose to define its content entirely, like in this case:

```js
Vue.component('user-name', {
  props: ['name'],
  template: '<p>Hi {{ name }}</p>'
})
```

or it can also let the parent component inject any kind of content into it, by using **slots**.

What's a slot?

You define it by putting `<slot></slot>` in a component template:

```js
Vue.component('user-information', {
  template: '<div class="user-information"><slot></slot></div>'
})
```

When using this component, any content added between the opening and closing tag will be added inside the slot placeholder:

```html
<user-information>
  <h2>Hi!</h2>
  <user-name name="Flavio">
</user-information>
```

If you put any content side the `<slot></slot>` tags, that serves as the default content in case nothing is passed in.

A complicated component layout might require a better way to organize content.

Enter **named slots**.

With a named slot you can assign parts of a slot to a specific position in your component template layout, and you use a `slot` attribute to any tag, to assign content to that slot.

Anything outside any template tag is added to the main `slot`.

For convenience I use a `page` single file component in this example:

```html
<template>
  <div>
    <main>
      <slot></slot>
    </main>
    <sidebar>
      <slot name="sidebar"></slot>
    </sidebar>
  </div>
</template>
```

```html
<page>
  <ul slot="sidebar">
    <li>Home</li>
    <li>Contact</li>
  </ul>

  <h2>Page title</h2>
  <p>Page content</p>
</page>
```
