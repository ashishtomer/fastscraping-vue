# VUE.js Cheatsheet

## Vue Instance:

This controls the part(s) of our application

A vue instance is created with 

```
new Vue(
  {
    //JS Object
  }
);
```

We generally have a single 'root' vue instance, in single page application.

- In the root instance, we manage the hierarchy of components.
- Components can be called on demand by a user action - generally a URL.

We load our root component in the HTML page inside an HTML tag. I prefer a <div> tag with an html ID.


In the index.html:
```
  <body>
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
```
In the root component:
```
new Vue(
  {
    el: '#vue-app',
    data: {

    }
  }
)
```
or in main.js:
```
import Vue from 'vue'
import App from './App.vue'
import VueResource from 'vue-resource'

Vue.use(VueResource);

new Vue({
  render: h => h(App)
}).$mount('#app')
```

## Data and Function bindings (in Vue component):

In the root component we can define several things like data and methods inside the single JS object like this:
```
new Vue(
  {
    el: '#vue-app',
    data: {
      var1: 10
    },
    methods: {
      greet: function(name) {
        return 'Good morning ' + name;
      }
    }
  }
)
```

The data can be bound with  `{{}}` and methods can be called as usual like greet('Ashish'),  in the html page.

We can bind a lot of different kind of values like an `href` of anchor tag `<a>`, value of `<input>` tag with `v-bind:<kind of bind variable>`. We can bind html in the page also with `v-html='varible-name-containing-html-text'`.

We access the variable (declared in data object) in the functions with **this**.*variableName*

## Events:

We listen to events with **v-on**:*event-name*. Like -

```
<button v-on:click="greet('Ashish')">Greet User</button>
``` 

## Event modifiers:

We can define several event modifiers on the events (https://vuejs.org/v2/guide/events.html#Event-Modifiers)

This is the list:

    .stop
    .prevent
    .capture
    .self
    .once
    .passive

We define the event modifiers like this:

**v-on**:*event-name*.***event_modifier***

Example: `v-on:click.once="greet('Ashish')"`

## Two way data binding:

Whenever we change a variable on HTML page we can reflect that value back in the variable declared in the `data: {}`. We do this with `v-model="variableName"`. `{{}}` only injects the variable as a value in HTML - once.

## Computed properties:


```
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
```
```
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // a computed getter
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
})
```

Here we have declared a computed property `reversedMessage`. The function we provided will be used as the getter function for the property `vm.reversedMessage`:

```
console.log(vm.reversedMessage) // => 'olleH'
vm.message = 'Goodbye'
console.log(vm.reversedMessage) // => 'eybdooG'
```

You may have noticed we can achieve the same result by invoking a method in the expression:

```
<p>Reversed message: "{{ reverseMessage() }}"</p>
```
```
// in component
methods: {
  reverseMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```

Computed properties are cached based on their reactive dependencies. **A computed property will only re-evaluate when some of its reactive dependencies have changed**. This means as long as message has not changed, multiple access to the `reversedMessage` computed property will immediately return the previously computed result without having to run the function again.

This also means the following computed property will never update, because Date.now() is not a reactive dependency:

```
computed: {
  now: function () {
    return Date.now()
  }
}
```

Why do we need caching? Imagine we have an expensive computed property A, which requires looping through a huge Array and doing a lot of computations. Then we may have other computed properties that in turn depend on A. Without caching, we would be executing A’s getter many more times than necessary! In cases where you do not want caching, use a method instead.

## Binding CSS classes

We can bind the class to a variable with `v-bind:class="{<className1>:<true/false>, <className2>:<true/false>}"`. Here we can assign true or false direct to class name. But doing this, we can't change the class name on runtime. To do that, assign a variable to className like `className1:variableContainingClassNameString`. Now change the `variableContainingClassNameString` to `true` or `false` based on user action. `false` value will remove particular class and `true` will make the class active.

## Conditionals `v-if` and `v-show`

These tags are used to display and hide/remove the particular tag from HTML page.

`v-if` takes a boolean value. It true, the tag will be in the page, if false, then it'll be removed completely from the page's HTML tree.

```
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else-if="average">Angular is average!</h1>
<h1 v-else>Oh no 😢</h1>
```

`v-show` will set the display style property to true/none.

## v-for (https://vuejs.org/v2/guide/list.html)
We can iterate on an array right in the HTML page.

```
<ul id="example-1">
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
</ul>
```
```
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

`v-for` also supports an optional second argument for the index of the current item.

```
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```
You can also use v-for to iterate through the properties of an object.
```
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

*When iterating over an object, the order is based on the enumeration order of `Object.keys()`, which is not guaranteed to be consistent across JavaScript engine implementations.*

## Multiple Vue instances

Inside the app.js, we can define more than one instance - which can render in there respenctive `<div>` tags using the id assigned to the div and using that in el of instance. It's not advised to render mumltiple instance though.

## Vue component

We can declare a component in the app.js like this -

```
Vue.component('compName', {
  template: '<html section to be loaded in the component>'
})
```
Now we can render the component in the vue instance like this

```
  <body>
    <div id="app">
      <compName></compName>
    </div>
  </body>
```
Component declared by `Vue.component()` is a global component and can be used in any instance.

------------------------------

The data object can be declared in the component
```
Vue.component('compName', {
  template: '<html section to be loaded in the component>',
  data: function() {

  }
})
```

data is defined as function so that data is local to one declaration of the component.

```
// Define a new component called button-counter
Vue.component('button-counter', {
  data: function () {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="count++">You clicked me {{ count }} times.</button>'
})
```
Components can be reused as many times as you want:
```
<div id="components-demo">
  <button-counter></button-counter>
  <button-counter></button-counter>
  <button-counter></button-counter>
</div>
```
[**data** Must Be a Function](https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function)

## Create project with vue/cli

Using the vue cli can setup a VUE.JS project. The project then can organize the project in component files (.vue files) with a single root component being used in the single vue instance.

First install node.js and then install vue-cli using **npm**
`npm install -g @vue/cli` // This is newer version's name

You can check you have the right version with this command:
`vue --version`

To upgrade the global Vue CLI package, you need to run:
`npm update -g @vue/cli`

To create a new project, run:
`vue create hello-world`

The new project created will have folders *node_modules* and *src* along with *.babelrc* *index.html*, *README.md* and *webpack.config.js*

These files are the bones of a vue application.

## Vue files and root component

Inside the *src* directory we've *assets* directory and JS files *App.vue* and *main.js*

*main.js* controls everything from the start. This file imports `App from App.vue`. This App is the root component which is used to create the **vue instance** and **render** on html page `index.html`.

We can render our root component in two ways (both are same):

```
new Vue(
  {
    el: '#app', //any html tab which can render the App
    render: h => h(App)
  }
)
```
Or,
```
new Vue({
  render: h => h(App)
}).$mount('#app')
```

## Vue Component Revisited
In the project created by vue-cli, the components are created in the .vue files (.vue is just convention).
In these files, the code is devided in three parts -
```
<template>
  <!-- The HTML part to be rendered -->
</template>

<script type="text/javascript">
  //imports here

  export default {
    components: {

    },

    data: function() {

    },

    methods: {

    },

    computed: {

    }
  }
</script>

<style type="text/css" scoped>
  
</style>
```

So a component:
- represents a part of whole webpage. 
- contains HTML, CSS and Javascript code to render the intended part

## Nesting a component in another component

We can nest one component in another by registering a component globally in `main.js` or importing in the parent component where we want to nest it.

Let's say we've `ninjas.vue`. It defines and exports a component.

**We can register the component globally in `main.js`:**

```
import Ninjas from './ninjas.vue'
Vue.component('ninjas', Ninjas) //first one is name we give it, seconds is object (which we export in .vue file)
```

Now we can render this in any component's template like this:

```
<template>
  <div> <!-- template should have a root HTML tag -->
    <ninjas></ninjas> <!-- component renders here. tag name is same as name given to it while registering -->
  </div>
</template>
```

**We can import the component locally in a target component:**

Now we can render this in targeted component's template like this:
```
<template>
  <div> <!-- template should have a root HTML tag -->
    <ninjas></ninjas> <!-- component renders here. tag name is same as name given to it while registering -->
  </div>
</template>

<script type="text/javascript">
  //imports here
  import Ninjas from './ninjas.vue';

  export default {
    components: {
      'ninjas' : Ninjas //Locally giving name to imported nested component. It's actually local registration.
    }
    data: function() {

    },

    methods: {

    },

    computed: {

    }
  }
</script>
```

## HTTP Requests with Vue

Vue itself doesn't provide support to do HTTP requests. We can install and import the plugin(s) to do that.
I am going to use [**VueResource**](https://github.com/pagekit/vue-resource). We can use jQuery or fetch api of JS/browsers also.

Install it:

```
npm install vue-resource --save
```
After installation, it'll be in `package.json`'s dependencies.

Import in `main.js`:

```
import VueResource from 'vue-resource'

Vue.use(VueResource); //Very important. Vue.use() makes the plugins available to be used.
```

Using the VueResource to make requests:
In the template:
```
<button v-on:click.prevent="pastForm()">Add Blog</button>
```
In the script-
```
<script type="text/javascript">
  export default {
    data: function() {
      blog: {
        title: "",
        content: ""
      },
      submitted: false
    },

    methods: {
      postForm: function() {
        this.$http.post('https://example.com/v1/api/add/blog', {
          title: this.blog.title,
          body: this.blog.content,
          userId: 1
        }).then(function(data) {
          console.log(data);
          this.submitted = true;
        })
      }
    }
  }
</script>
```

## Routing with vue

Plugin to use : **vue-router**

Define a `routes.js` under the **/src**, and declare your routes.

```
import showBlogs from './components/showBlogs.vue';
import addBlogs from './components/addBlogs.vue';

export default [
  {
    path: '/',
    component: showBlog
  },

  {
    path: '/add',
    component: addBlog
  }
]
```

Now register these routes with router instance in `main.js`.

```
import VueRouter from 'vue-router';
import Routes from './routes'; //We defined the file above

Vue.use(VueRouter);

const myRouter = new VueRouter({
  routes: Routes
})

new Vue({
  el: '#app',
  render: h => h(App),
  router: myRouter
})

```
