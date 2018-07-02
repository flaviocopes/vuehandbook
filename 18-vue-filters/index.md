Filters are a functionality provided by Vue components that let you apply formatting and transformations to any part of your template dynamic data.

They don't change a component data or anything, but they only affect the output.

Say you are printing a name:

```html
<template>
  <p>Hi {{ name }}!</p>
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

What if you want to check that `name` is actually containing a value, and if not print 'there', so that our template will print "Hi there!"?

Enter filters:

```html
<template>
  <p>Hi {{ name | fallback }}!</p>
</template>

<script>
export default {
  data() {
    return {
      name: 'Flavio'
    }
  },
  filters: {
    fallback: function(name) {
      return name ? name : 'there'
    }
  }
}
</script>
```

Notice the syntax to apply a filter, which is `| filterName`. If you're familiar with Unix, that's the Unix pipe operator, which is used to pass the output of an operation as an input to the next one.

The `filters` property of the component is an object. A single filter is a function that accepts a value and returns another value.

The returned value is the one that's actually printed in the Vue.js template.

The filter, of course, has access to the component data and methods.

What's a good use case for filters?

- transforming a string, for example, capitalizing or making it lowercase
- formatting a price

Above you saw a simple example of a filter: `{{ name | fallback }}`.

Filters can be chained, by repeating the pipe syntax:

```js
{{ name | fallback | capitalize }}
```

This first applies the `fallback` filter, then the `capitalize` filter (which we didn't define, but try making one!).

Advanced filters can also accept parameters, using the normal function parameters syntax:

```html
<template>
  <p>Hello {{ name | prepend('Dr.') }}</p>
</template>

<script>
export default {
  data() {
    return {
      name: 'House'
    }
  },
  filters: {
    prepend: (name, prefix) => {
      return `${prefix} ${name}`
    }
  }
}
</script>
```

If you pass parameters to a filter, the first one passed to the filter function is always the item in the template interpolation (`name` in this case), followed by the explicit parameters you passed.

You can use multiple parameters by separating them using a comma.

Notice I used an arrow function. We avoid arrow function in methods and computed properties generally because they almost always reference `this` to access the component data, but in this case, the filter does not need to access this but receives all the data it needs through the parameters, and we can safely use the simpler arrow function syntax.

[This package](https://www.npmjs.com/package/vue2-filters) has a lot of pre-made filters for you to use directly in templates, which include `capitalize`, `uppercase`, `lowercase`, `placeholder`, `truncate`, `currency`, `pluralize` and more.
