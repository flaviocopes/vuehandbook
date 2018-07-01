Vue is a very popular JavaScript frontend framework, one that's experiencing a huge growth.

It is simple, tiny (~24KB) and very performant. It feels different from all the other JavaScript frontend frameworks and view libraries. Let's find out why.

## First, what is a JavaScript frontend framework?

If you're unsure what a JavaScript framework is, Vue is the perfect first encounter with one.

A JavaScript framework helps us create modern applications. Modern JavaScript applications are mostly used on the Web, but also power a lot of Desktop and Mobile applications.

Until the early 2000s, browsers didn't have the capabilities they have now. They were a lot less powerful, and building complex applications inside them was not feasible by the point of view of performance, and the tooling was not even something that people thought about.

Everything changed when Google unveiled Google Maps and GMail, two applications that ran inside the browser. Ajax made asynchronous network requests possible, and over time developers started building on top of the Web platform, while engineers worked on the platform itself: browsers, the Web standards, the browser APIs, and the JavaScript language.

Libraries like jQuery and Mootools were the first big projects that built upon JavaScript, and were hugely popular for a while. They basically provided a nicer API to interact with the browser, and provided workarounds for bugs and inconsistencies among the various browsers.

Frameworks like Backbone, Ember, Knockout, AngularJS were the first wave of modern JavaScript frameworks. The second wave, which is the current one, has React, Angular and Vue as its main actors.

> Note that jQuery, Ember and the other projects I mentioned are still being heavily used, actively maintained, and millions of websites rely on them. That said, techniques and tools evolve, and as a JavaScript developer, you're now likely to be required to know React, Angular or Vue than those older frameworks.

Frameworks abstract the interaction with the browser and the DOM. Instead of manipulating elements by referencing them in the DOM, we **declaratively** define and interact with them, at a higher level.

Using a framework is like using the C programming language instead of using the Assembly language to write system programs. It's like using a computer to write a document instead of using a typewriter. It's like having a self-driving car instead of driving the car yourself.

Well, not that far, but you get the idea. Instead of using low-level APIs offered by the browser to manipulate elements, and build hugely complex systems to write an application, **you use tools built by very smart people that make our life easier**.

## The popularity of Vue

How much popular is Vue.js?

Vue had:

- 7600 stars on GitHub in 2016
- 36700 stars on GitHub in 2017

and it has more than 100.000+ stars on GitHub, as of June 2018

Its npm download count is growing every day, and now it's at ~350.000 downloads per week.

I would say Vue is **a lot popular**, given those numbers.

In relative terms, it has approximately the same numbers of GitHub stars of React, which was born years earlier.

Numbers are not everything, of course. The impression I have of Vue is that developers _love_ it.

A key point in time of the rise of Vue has been the adoption in the Laravel ecosystem, a hugely popular PHP web application framework, but since then it has widespread among many other development communities.

## Why developers love Vue

First, Vue is called a **progressive framework**.

This means that it adapts to the needs of the developer. While other frameworks requiring a complete buy-in from a developer or team, and often want you to rewrite an existing application because they requires some specific set of conventions, Vue happily lands inside your app with a simple `script` tag, to start with, and it can grow along with your needs, spreading from 3 lines to managing your entire view layer.

You don't need to know about webpack, Babel, npm or anything to get started with Vue, but when you're ready Vue makes it simple for you to rely on them.

This is one great selling point, especially in the current ecosystem of JavaScript frontend frameworks and libraries that tends to alienate newcomers and also experienced developers that feel lost in the ocean of possibilities and choices.

Vue.js is probably the more approachable frontend framework around. Some people call Vue the _new jQuery_, because it easily gets in the application via a script tag, and gradually gains space from there. Think of it as a compliment, since jQuery dominated the Web in the past few years, and it still does its job on a huge number of sites.

Vue picks from the best ideas. It was built by picking the best ideas of frameworks like Angular, React and Knockout, and by cherry-picking the best choices those frameworks made, and excluding some less brilliant ones, it kind of started as a "best-of" set and grew from there.

## Where does Vue.js position itself in the frameworks landscape

The 2 elephants in the room, when talking about web development, are **React** and **Angular**. How does Vue position itself relatively to those 2 big and popular frameworks?

Vue was created by Evan You when he was working at Google on AngularJS (Angular 1.0) apps, and was born out of a need to create more performant applications. Vue picked some of the Angular templating syntax, but removed the opinionated, complex stack that Angular required, and made it very performant.

The new Angular (Angular 2.0) also solved many of the AngularJS issues, but in very different ways, and requires a buy-in to TypeScript which not all developers enjoy using (or care learning).

What about React? Vue took many good ideas from React, most importantly the Virtual DOM. But Vue implements it with some sort of automatic dependency management, which tracks which components are affected by a change of the state, so that only those components are re-rendered when that state property changes. In React on the other hand when a part of the state that affects a component, the component will be re-rendered and by default all its children will be rerendered as well. To avoid this you need to use the shouldComponentUpdate method of each component and determine if that component should be rerendered. This gives Vue a bit of advantage in terms of ease of use, and out of the box performance gains.

One big difference with React is JSX. While you can technically use JSX in Vue, it's not a popular approach and instead the templating system is used. Any HTML file is a valid Vue template, while JSX is very different than HTML and has a learning curve for people in the team that might only need to work with the HTML part of your app, like designers. Vue templates are a lot similar to Mustache and Handlebars (although they differ in terms of flexibility) and as such they are more familiar to developers that already used frameworks like Angular and Ember.

The official state management library, Vuex, follows the Flux architecture and is somewhat similar to Redux in its concepts. Again, this is part of the positive things about Vue, which saw this good pattern in React and borrowed it to its ecosystem. And while you can use Redux with Vue, Vuex is specifically tailored for Vue and its inner workings.

Vue is flexible but the fact that the core team maintains two packages very important for any web app like routing and state management makes it a lot less fragmented than React for example: `vue-router` and `vuex` are key to the success of Vue. You don't need to choose or worry if that library you chose is going to be maintained in the future and will keep up with framework updates, and being official they are the canonical go-to libraries for their niche (but you can choose to use what you like, of course).

One thing that puts Vue in a different bucket compared to React and Angular is that Vue is an _indie_ project: it's not backed by a huge corporation like Facebook or Google. Instead, it's completely backed by the community, which fosters development through donations and sponsoring. This makes sure the roadmap of Vue is not driven by a single company agenda.
