## Introduction

In a JavaScript web application, a router is the part that syncs the current displayed view with the browser address bar content.

In other words, it's the part that makes the URL change when you click something in the page, and also helps showing the correct view when you hit a specific URL.

Traditionally the Web is built around URLs. When you hit a certain URL, a specific page is displayed.

With the introduction of applications that run inside the browser and change what the user sees, many applications broke this interaction, and you had to manually update the URL with the browser's History API.

You need a router when you need to sync URLs to views in your app. It's a very common need, and all the major modern frameworks now allow you to manage routing.

The Vue Router library is the way to go for Vue.js applications. Vue does not enforce the use of this library. You can use whatever generic routing library you want, or also create your own History API integration, but the benefit of using Vue Router is that it's **official**.

This means it's maintained by the same people that maintain Vue, so you get a more consistent integration in the framework, and the guarantee that it's always going to be compatible in the future, no matter what.

## Installation

Vue Router is available via npm with the package named `vue-router`.

If you use Vue via a script tag, you can include Vue Router using

```html
<script src="https://unpkg.com/vue-router"></script>
```

> unpkg.com is a very handy tool that makes every npm package available in the browser with a simple link

If you use the Vue CLI, install it using

```bash
npm install vue-router
```

Once you install `vue-router` and make it available either using a script tag or via Vue CLI, you can now import it in your app.

You import it after `vue`, and you call `Vue.use(VueRouter)` to _install_ it inside the app:

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)
```

After you call `Vue.use()` passing the router object, in any component of the app you have access to these objects:

- `this.$router` is the router object
- `this.$route` is the current route object

## The router object

The router object, accessed using `this.$router` from any component when the Vue Router is installed in the root Vue component, offers many nice features.

We can make the app navigate to a new route using

- `this.$router.push()`
- `this.$router.replace()`
- `this.$router.go()`

which resemble the `pushState`, `replaceState` and `go` methods of the History API.

`push()` is used to go to a new route, adding a new item to the browser history. `replace()` is identical in usage, except it does not push a new state to the history.

Usage samples:

```js
this.$router.push('about') //named route, see later
this.$router.push({ path: 'about' })
this.$router.push({ path: 'post', query: { post_slug: 'hello-world' } }) //using query parameters (post?post_slug=hello-world)
this.$router.replace({ path: 'about' })
```

`go()` goes back and forth, accepting a number that can be positive or negative to go back in the history:

```js
this.$router.go(-1) //go back 1 step
this.$router.go(1) //go forward 1 step
```

## Defining the routes

I'm using a Vue Single File Component in this example.

In the template I use a `nav` tag that contains 3 `router-link` components, which have a label (Home/Login/About) and a URL assigned through the `to` attribute.

The `router-view` component is where the Vue Router will put the content that matches the current URL.

```html
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/login">Login</router-link>
      <router-link to="/about">About</router-link>
    </nav>
    <router-view></router-view>
  </div>
</template>
```

A `router-link` component renders an `a` tag by default (you can change that). Every time the route changes, either by clicking a link or by changing the URL, a `router-link-active` class is added to the element that refers to the active route, allowing you to style it.

In the JavaScript part we first include and install the router, then we define 3 **route components**.

We pass them to the initialization of the `router` object, and we pass this object to the Vue root instance.

Here's the code:

```html
<script>
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(Router)

const Home  = {
  template: '<div>Home</div>'
}

const Login = {
  template: '<div>Login</div>'
}

const About = {
  template: '<div>About</div>'
}

const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/login', component: Login },
    { path: '/about', component: About }
  ]
})

new Vue({
  router
}).$mount('#app')
</script>
```



Usually in a Vue app, you instantiate and mount the root app using:

```js
new Vue({
  render: h => h(App)
}).$mount('#app')
```

When using the Vue Router, you don't pass a `render` property, but instead you use `router`.

The syntax used in the above example:

```js
new Vue({
  router
}).$mount('#app')
```

is a shorthand for

```js
new Vue({
  router: router
}).$mount('#app')
```

See, in the example we pass a `routes` array to the `VueRouter` constructor. Each route in this array has a `path` and `component` params.

If you pass a `name` param too, you have a **named route**.

## Using named routes to pass parameters to the router push and replace methods

Remember how we used the Router object to push a new state previously?

```js
this.$router.push({ path: 'about' })
```

With a named route we can pass parameters to the new route:

```js
this.$router.push({ name: 'post', params: { post_slug: 'hello-world' } })
```

the same goes for `replace()`:

```js
this.$router.replace({ name: 'post', params: { post_slug: 'hello-world' } })
```

## What happens when a user clicks a `router-link`

The application will render the route component that matches the URL passed to the link.

The new route component that handle the URL is instantiated and its guards called, and the old route component will be destroyed.

## Route guards

Since we mentioned **guards**, let's introduce them.

You can think of them of lifecycle hooks or middleware, those are functions called at specific times during the execution of the application. You can jump in and alter the execution of a route, redirecting or simply cancelling the request.

You can have global guards by adding a callback to the `beforeEach()` and `afterEach()` property of the router.

- `beforeEach()` is called before the navigation is confirmed
- `beforeResolve()` is called when beforeEach is executed and all the components `beforeRouterEnter` and `beforeRouteUpdate` guards are called, but before the navigation is confirmed. The final check, if you want
- `afterEach()` is called after the navigation is confirmed

What does "the navigation is confirmed" mean? We'll see it in a second. In the meantime think of it as "the app can go to that route".

The usage is:

```js
this.$router.beforeEach((to, from, next) => {
  // ...
})
```

```js
this.$router.afterEach((to, from) => {
  // ...
})
```

`to` and `from` represent the route objects that we go to and from. `beforeEach` has an additional parameter `next` which if we call with `false` as the parameter, will block the navigation, and cause it to be unconfirmed. Like in Node middleware, if you're familiar, next() should always be called otherwise execution will get stuck.

Single route components also have guards:

- `beforeRouteEnter(from, to, next)` is called before the current route is confirmed
- `beforeRouteUpdate(from, to, next)` is called when the route changes but the component that manages it is still the same (with dynamic routing, see next)
- `beforeRouteLeave(from, to, next)` is called when we move away from here

We mentioned navigation. To determine if the navigation to a route is confirmed, Vue Router performs some checks:

- it calls `beforeRouteLeave` guard in the current component(s)
- it calls the router `beforeEach()` guard
- it calls the `beforeRouteUpdate()` in any component that needs to be reused, if any exist
- it calls the `beforeEnter()` guard on the route object (I didn't mention it but you can look [here](https://router.vuejs.org/guide/advanced/navigation-guards.html#per-route-guard))
- it calls the `beforeRouterEnter()` in the component that we should enter into
- it calls the router `beforeResolve()` guard
- if all was fine, the navigation is confirmed!
- it calls the router `afterEach()` guard

You can use the route-specific guards (`beforeRouteEnter` and `beforeRouteUpdate` in case of dynamic routing) as lifecycle hooks, so you can start **data fetching requests** for example.

## Dynamic routing

The example above shows a different view based on the URL, handling the `/`, `/login` and `/about` routes.

A very common need is to handle dynamic routes, like having all posts under `/post/`, each with the slug name:

- `/post/first`
- `/post/another-post`
- `/post/hello-world`

You can achieve this using a dynamic segment.

Those were static segments:

```js
const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/login', component: Login },
    { path: '/about', component: About }
  ]
})
```

we add in a dynamic segment to handle blog posts:

```js
const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/post/:post_slug', component: Post },
    { path: '/login', component: Login },
    { path: '/about', component: About }
  ]
})
```

Notice the `:post_slug` syntax. This means that you can use any string, and that will be mapped to the `post_slug` placeholder.

You're not limited to this kind of syntax. Vue relies on [this library](https://github.com/pillarjs/path-to-regexp) to parse dynamic routes, and you can go wild with Regular Expressions.

Now inside the Post route component we can reference the route using `$route`, and the post slug using `$route.params.post_slug`:

```js
const Post = {
  template: '<div>Post: {{ $route.params.post_slug }}</div>'
}
```

We can use this parameter to load the contents from the backend.

You can have as many dynamic segments as you want, in the same URL:

`/post/:author/:post_slug`

Remember when before we talked about what happens when a user navigates to a new route?

In the case of dynamic routes, what happens is a little different.

Vue to be more efficient instead of destroying the current route component and re-instantiating it, it reuses the current instance.

When this happens, Vue calls the `beforeRouteUpdate` lifecycle event. There you can perform any operation you need:

```js
const Post = {
  template: '<div>Post: {{ $route.params.post_slug }}</div>'
  beforeRouteUpdate(to, from, next) {
    console.log(`Updating slug from ${from} to ${to}`)
    next() //make sure you always call next()
  }
}
```

## Using props

In the examples up to now I used `$route.params.*` to access the route data. A component should not be so tightly coupled with the router, and instead we can use props:

```js
const Post = {
  props: ['post_slug'],
  template: '<div>Post: {{ post_slug }}</div>'
}

const router = new VueRouter({
  routes: [
    { path: '/post/:post_slug', component: Post, props: true }
  ]
})
```

Notice the `props: true` passed to the route object to enable this functionality.

## Nested routes

Before I mentioned that you can have as many dynamic segments as you want, in the same URL, like:

`/post/:author/:post_slug`

So, say we have an Author component taking care of the first dynamic segment:

```html
<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(Router)

const Author  = {
  template: '<div>Author: {{ $route.params.author}}</div>'
}

const router = new VueRouter({
  routes: [
    { path: '/post/:author', component: Author }
  ]
})

new Vue({
  router
}).$mount('#app')
</script>
```

We can insert a second `router-view` component instance inside the Author template:

```js
const Author  = {
  template: '<div>Author: {{ $route.params.author}}<router-view></router-view></div>'
}
```

we add the Post component:

```js
const Post = {
  template: '<div>Post: {{ $route.params.post_slug }}</div>'
}
```

and then we'll inject the inner dynamic route in the VueRouter configuration:

```js
const router = new VueRouter({
  routes: [{
    path: '/post/:author',
    component: Author,
    children: [
      path: ':post_slug',
      component: Post
    ]
  }]
})
```
