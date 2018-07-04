Props are the way components can accept data from components that include them (parent components).

When a component expects one or more prop, it must define them in its `props` property:

```js
Vue.component('user-name', {
  props: ['name'],
  template: '<p>Hi {{ name }}</p>'
})
```

or, in a Vue Single File Component:

```html
<template>
  <p>{{ name }}</p>
</template>

<script>
export default {
  props: ['name']
}
</script>
```

## Accept multiple props

You can have multiple props by simply appending them to the array:

```js
Vue.component('user-name', {
  props: ['firstName', 'lastName'],
  template: '<p>Hi {{ firstName }} {{ lastName }}</p>'
})
```

## Set the prop type

You can specify the type of a prop very simply by using an object instead of an array, using the name of the property as the key of each property, and the type as the value:

```js
Vue.component('user-name', {
  props: {
    firstName: String,
    lastName: String
  },
  template: '<p>Hi {{ firstName }} {{ lastName }}</p>'
})
```

The valid types you can use are:

- String
- Number
- Boolean
- Array
- Object
- Date
- Function
- Symbol

When a type mismatches, Vue alerts (in development mode) in the console with a warning.

Prop types can be more articulated.

You can allow multiple different value types:

```js
props: {
  firstName: [String, Number]
}
```

## Set a prop to be mandatory

You can require a prop to be mandatory:

```js
props: {
  firstName: {
    type: String,
    required: true
  }
}
```

## Set the default value of a prop

You can specify a default value:

```js
props: {
  firstName: {
    type: String,
    default: 'Unknown person'
  }
}
```

For objects:

```js
props: {
  name: {
    type: Object,
    default: {
      firstName: 'Unknown',
      lastName: ''
    }
  }
}
```

`default` can also be a function that returns an appropriate value, rather than being the actual value.

You can even build a custom validator, which is cool for complex data:

```js
props: {
  name: {
    validator: name => {
      return name === 'Flavio' //only allow "Flavios"
    }
  }
}
```

## Passing props to the component

You pass a prop to a component using the syntax

```html
<ComponentName color="white" />
```

if what you pass is a static value.

If it's a data property, you use

```html
<template>
  <ComponentName :color=color />
</template>

<script>
...
export default {
  //...
  data: function() {
    return {
      color: 'white'
    }
  },
  //...
}
</script>
```

You can use a ternary operator inside the prop value to check a truthy condition and pass a value that depends on it:

```html
<template>
  <ComponentName :colored="color == 'white' ? true : false" />
</template>

<script>
...
export default {
  //...
  data: function() {
    return {
      color: 'white'
    }
  },
  //...
}
</script>
```
