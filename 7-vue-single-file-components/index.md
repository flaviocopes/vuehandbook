A Vue component can be declared in a JavaScript file (`.js`) like this:

```js
Vue.component('component-name', {
  /* options */
})
```

or also:

```js
new Vue({
  /* options */
})
```

or it can be specified in a `.vue` file.

The `.vue` file is pretty cool because it allows you to define

- JavaScript logic
- HTML code template
- CSS styling

all in just a single file, and as such it got the name of **Single File Component**.

Here's an example:

```html
<template>
  <p>{{ hello }}</p>
</template>

<script>
export default {
  data() {
    return {
      hello: 'Hello World!'
    }
  }
}
</script>

<style scoped>
  p {
    color: blue;
  }
</style>
```

All or this is possible thanks to the use of webpack. The Vue CLI makes this very easy and supported out of the box. `.vue` files cannot be used without a webpack setup, and as such they are not very suited to apps that just use Vue on a page without being a full-blown single-page app (SPA).

Since Single File Components rely on Webpack, we get for free the ability to use modern Web features.

Your CSS can be defined using SCSS or Stylus, the template can be built using Pug, and all you need to do to make this happen is to declare to Vue which language preprocessor you are going to to use.

The list of supported preprocessors include

- TypeScript
- SCSS
- Sass
- Less
- PostCSS
- Pug

We can use modern JavaScript (ES6-7-8) regardless of the target browser, using the Babel integration, and ES Modules too, so we can use `import/export` statements.

We can use CSS Modules to scope our CSS.

Speaking of scoping CSS, Single File Components make it absolutely easy to write CSS that won't _leak_ to other components, by using `<style scoped>` tags.

If you omit `scoped`, the CSS you define will be global. But adding that, Vue adds automatically a specific class to the component, unique to your app, so the CSS is guaranteed to not leak out to other components.

Maybe your JavaScript is huge because of some logic you need to take care of. What if you want to use a separate file for your JavaScript?

You can use the `src` attribute to externalize it:

```html
<template>
  <p>{{ hello }}</p>
</template>
<script src="./hello.js"></script>
```

This also works for your CSS:

```html
<template>
  <p>{{ hello }}</p>
</template>
<script src="./hello.js"></script>
<style src="./hello.css"></style>
```

Notice how I used

```js
export default {
  data() {
    return {
      hello: 'Hello World!'
    }
  }
}
```

in the component JavaScript to set up the data.

Other common ways you will see are

```js
export default {
  data: function() {
    return {
      name: 'Flavio'
    }
  }
}
```

(the above is equivalent to what we did before)

or:

```js
export default {
  data: () => {
    return {
      name: 'Flavio'
    }
  }
}
```

this is different because it uses an arrow function. Arrow functions are fine until we need to access a component method, as we need to make use of `this` and such property is not bound to the component using arrow functions. So it's mandatory to use _regular_ functions rather than arrow functions.

You might also see

```js
module.exports = {
  data: () => {
    return {
      name: 'Flavio'
    }
  }
}
```

this is using the CommonJS syntax, and works as well, although it's recommended to use the ES Modules syntax, as that is a JavaScript standard.
