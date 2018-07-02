Now that you know about methods, watchers and computed properties, you might be wondering when should you use one vs the others.

Here's a breakdown of this question.

## When to use methods

- To react on some event happening in the DOM
- To call a function when something happens in your component. You can call a methods from computed properties or watchers.

## When to use computed properties

- You need to compose new data from existing data sources
- You have a variable you use in your template that's built from one or more data properties
- You want to reduce a complicated, nested property name to a more readable and easy to use one, yet update it when the original property changes
- You need to reference a value from the template. In this case, creating a computed property is the best thing because it's cached.
- You need to listen to changes of more than one data property

## When to use watchers

- You want to listen when a data property changes, and perform some action
- You want to listen to a prop value change
- You only need to listen to one specific property (you can't watch multiple properties at the same time)
- You want to watch a data property until it reaches some specific value and then do something
