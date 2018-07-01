The simplest option to add CSS to a Vue.js component is to use the `style` tag, just like in HTML:

```html
<template>
  <p style="text-decoration: underline">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      decoration: 'underline'
    }
  }
}
</script>
```

This is as much static as you can get. What if you want `underline` to be defined in the component data? Here's how you can do it:

```html
<template>
  <p :style="{'text-decoration': decoration}">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      decoration: 'underline'
    }
  }
}
</script>
```

`:style` is a shorthand for `v-bind:style`. I'll use this shorthand throughout this tutorial.

Notice how we had to wrap `text-decoration` in quotes. This is because of the dash, which is not part of a valid JavaScript identifier.

You can avoid the quote by using a special camelCase syntax that Vue.js enables, and rewriting it to `textDecoration`:

```html
<template>
  <p :style="{textDecoration: decoration}">Hi!</p>
</template>
```

Instead of binding an object to `style`, you can reference a computed property:

```html
<template>
  <p :style="styling">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      textDecoration: 'underline',
      textWeight: 'bold'
    }
  },
  computed: {
    styling: function() {
      return {
        textDecoration: this.textDecoration,
        textWeight: this.textWeight
      }
    }
  }
}
</script>
```

Vue components generate plain HTML, so you can choose to add a class to each element, and add a corresponding CSS selector with properties that style it:

```html
<template>
  <p class="underline">Hi!</p>
</template>

<style>
.underline { text-decoration: underline; }
</style>
```

You can use SCSS like this:

```html
<template>
  <p class="underline">Hi!</p>
</template>

<style lang="scss">
body {
  .underline { text-decoration: underline; }
}
</style>
```

You can hardcode the class like in the above example, or you can bind the class to a component property, to make it dynamic, and only apply that class if the data property is true:

```html
<template>
  <p :class="{underline: isUnderlined}">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      isUnderlined: true
    }
  }
}
</script>

<style>
.underline { text-decoration: underline; }
</style>
```

Instead of binding an object to class, like we did with `<p :class="{text: isText}">Hi!</p>`, you can directly bind a string, and that will reference a data property:

```html
<template>
  <p :class="paragraphClass">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      paragraphClass: 'underline'
    }
  }
}
</script>

<style>
.underline { text-decoration: underline; }
</style>
```

You can assign multiple classes either adding two classes to `paragraphClass` in this case, or by using an array:

```html
<template>
  <p :class="[decoration, weight]">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      decoration: 'underline',
      weight: 'weight',
    }
  }
}
</script>

<style>
.underline { text-decoration: underline; }
.weight { font-weight: bold; }
</style>
```

The same can be done using an object inlined in the class binding:

```html
<template>
  <p :class="{underline: isUnderlined, weight: isBold}">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      isUnderlined: true,
      isBold: true
    }
  }
}
</script>

<style>
.underline { text-decoration: underline; }
.weight { font-weight: bold; }
</style>
```

And you can combine the two statements:

```html
<template>
  <p :class="[decoration, {weight: isBold}]">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      decoration: 'underline',
      isBold: true
    }
  }
}
</script>

<style>
.underline { text-decoration: underline; }
.weight { font-weight: bold; }
</style>
```

You can also use a computed property that returns an object, which works best when you have many CSS classes to add at the same element:

```html
<template>
  <p :class="paragraphClasses">Hi!</p>
</template>

<script>
export default {
  data() {
    return {
      isUnderlined: true,
      isBold: true
    }
  },
  computed: {
    paragraphClasses: function() {
      return {
        underlined: this.isUnderlined,
        bold: this.isBold
      }
    }
  }
}
</script>

<style>
.underlined { text-decoration: underline; }
.bold { font-weight: bold; }
</style>
```

Notice that in the computed property you need to reference the component data using `this.[propertyName]`, while in the template data properties are conveniently put as first-level properties.

Any CSS that's not hardcoded like in the first example is going to be processed by Vue, and Vue does the nice job of automatically prefixing the CSS for us, so we can write clean CSS while still targeting older browsers (which still means browsers that Vue supports, so IE9+)
