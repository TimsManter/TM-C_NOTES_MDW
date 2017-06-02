# Vue.js

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-03
* @BasedOn: [Guide][basedon]

[basedon]: https://vuejs.org/v2/guide/

<!-- TOC -->

- [Overview](#overview)
- [Basic binding](#basic-binding)
- [Expressions](#expressions)
- [Bind](#bind)
  - [Basic bind](#basic-bind)
  - [Bind special attribute](#bind-special-attribute)
  - [Bind class to data](#bind-class-to-data)
  - [Bind class array to data](#bind-class-array-to-data)
  - [Bind style to data](#bind-style-to-data)
    - [Many properties](#many-properties)
    - [Single object](#single-object)
    - [Array](#array)
  - [Bind HTML](#bind-html)
- [Conditions](#conditions)
  - [If-else directives](#if-else-directives)
  - [If handlebars](#if-handlebars)
  - [If template](#if-template)
  - [Conditional show/hide](#conditional-showhide)
- [Loops](#loops)
  - [Bind `for` to `array`](#bind-for-to-array)
  - [Template](#template)
  - [Bind `for` to `object`](#bind-for-to-object)
  - [Range](#range)
  - [Mutation methods](#mutation-methods)
- [Input](#input)
  - [Events](#events)
    - [Modifiers](#modifiers)
  - [Fields](#fields)
- [Filters](#filters)
- [Components](#components)
  - [Local components](#local-components)
  - [`is` keyword](#is-keyword)
  - [Validation](#validation)
    - [Possible types](#possible-types)
  - [Dynamic components](#dynamic-components)
- [TypeScript](#typescript)
  - [Class Component](#class-component)
  - [Refs](#refs)

<!-- /TOC -->

## Basic binding

```html
<div id="app">
    {{ message }}
</div>
```

```js
var app = new Vue({
    el: '#app',
    data: {
        message: 'Hello Vue!'
    }
});
```

## Expressions

```html
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

## Bind

### Basic bind
```html
<!-- attribute bind with v-bind -->
<span v-bind:title="message">Sample</span>
<!-- alternative syntax -->
<span :title="message">Sample</span>
```

### Bind special attribute
```html
<span v-bind:id="dynamicId">Sample</span>

<button v-bind:disabled="dynamicDisabled">Button</button>
```

### Bind class to data
```html
<div class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
```

```js
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```

### Bind class array to data
```html
<div v-bind:class="[activeClass, errorClass]">
<div v-bind:class="[isActive ? activeClass : '', errorClass]">
<div v-bind:class="[{ active: isActive }, errorClass]">
```
```js
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

### Bind style to data

#### Many properties
```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```
```js
data: {
  activeColor: 'red',
  fontSize: 30
}
```
#### Single object
```html
<div v-bind:style="styleObject"></div>
```
```js
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

#### Array

```html
<div v-bind:style="[baseStyles, overridingStyles]">
```

### Bind HTML

```html
<!-- html bind with v-html -->
<div v-html="someCode"></div>
```

## Conditions

### If-else directives
```html
<!-- conditional presence of element -->
<h1 v-if="ok">Yes</h1>
<!-- optional else-if -->
<h1 v-else-if="maybe">Maybe</h1>
<!-- optional else -->
<h1 v-else>No</h1>
```

### If handlebars

```html
{{#if ok}}
  <h1>Yes</h1>
{{/if}}
```
### If template

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

### Conditional show/hide

```html
<h1 v-show="ok">Hello!</h1>
```

## Loops

### Bind `for` to `array`

```html
<!-- without index -->
<ul id="example">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>

<!-- with index -->
<ul id="example">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

```js
var example = new Vue({
  el: '#example',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

### Template

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```

### Bind `for` to `object`

```html
<!-- with value only -->
<ul id="repeat-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>

<!-- with key -->
<div v-for="(value, key) in object">
  {{ key }} : {{ value }}
</div>

<!-- with key and index -->
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }} : {{ value }}
</div>
```

```js
new Vue({
  el: '#repeat-object',
  data: {
    object: {
      firstName: 'John',
      lastName: 'Doe',
      age: 30
    }
  }
})
```

### Range

```html
<div>
  <span v-for="n in 10">{{ n }}</span>
</div>
```

### Mutation methods

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

## Input

### Events

```html
<div id="app">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
  <!-- alternative syntax -->
  <button @click="reverseMessage">Reverse Message</button>
</div>
```

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('');
    }
  }
});
```
#### Modifiers

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`

### Fields

```html
<div id="app">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```

```js
var app6 = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
});
```

## Filters

```html
<!-- in mustaches -->
{{ message | capitalize('arg1') | filterA }}

<!-- in v-bind -->
<div v-bind:id="rawId | formatId"></div>
```

```js
new Vue({
  // ...
  filters: {
    capitalize: function (value, arg1) {
      if (!value) return '';
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    }
  }
});
```

## Components

```js
Vue.component('todo-item', {
  template: '<li>This is a todo</li>',
  // optional properties when creating component
  props: ['todo']
  // data must be function
  data: function() { ... }
})
```

```html
<ol>
  <!-- create an instance of todo-item component -->
  <todo-item v-bind:todo="something"></todo-item>
</ol>
```

### Local components

```js
var Child = {
  template: '<div>A custom component!</div>'
}
new Vue({
  // ...
  components: {
    // <my-component> will only be available in parent's template
    'my-component': Child
  }
})
```

### `is` keyword

```html
<table>
  <tr is="my-row"></tr>
</table>
```

### Validation

```js
Vue.component('example', {
  props: {
    // basic type check (`null` means accept any type)
    propA: Number,
    // multiple possible types
    propB: [String, Number],
    // a required string
    propC: {
      type: String,
      required: true
    },
    // a number with default value
    propD: {
      type: Number,
      default: 100
    },
    // object/array defaults should be returned from a
    // factory function
    propE: {
      type: Object,
      default: function () {
        return { message: 'hello' }
      }
    },
    // custom validator function
    propF: {
      validator: function (value) {
        return value > 10
      }
    }
  }
})
```

#### Possible types

- String
- Number
- Boolean
- Function
- Object
- Array

### Dynamic components

```js
var vm = new Vue({
  el: '#example',
  data: {
    currentView: 'home'
  },
  components: {
    home: { /* ... */ },
    posts: { /* ... */ },
    archive: { /* ... */ }
  }
})
```

```html
<component v-bind:is="currentView">
  <!-- component changes when vm.currentView changes! -->
</component>
```

```js
var Home = {
  template: '<p>Welcome home!</p>'
}
var vm = new Vue({
  el: '#example',
  data: {
    currentView: Home
  }
})
```

## TypeScript

> Note: Vue.js already has TypeScript support.

### Class Component

> Note: Needs `vue-class-component` and optionally `vue-typescript-import-dts`.

```html
<template>
  <div>
    <input v-model="msg">
    <p>prop: {{propMessage}}</p>
    <p>msg: {{msg}}</p>
    <p>helloMsg: {{helloMsg}}</p>
    <p>computed msg: {{computedMsg}}</p>
    <button @click="greet">Greet</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from '../lib/index'
@Component({
  props: {
    propMessage: String
  }
})
export default class App extends Vue {
  propMessage: string
  // inital data
  msg: number = 123
  // use prop values for initial data
  helloMsg: string = 'Hello, ' + this.propMessage
  // lifecycle hook
  mounted () {
    this.greet()
  }
  // computed
  get computedMsg () {
    return 'computed ' + this.msg
  }
  // method
  greet () {
    alert('greeting: ' + this.msg)
  }
}
</script>
```

### Refs

```ts
// <some-component ref="myComp"></some-components>
// <some-component ref="myOtherComp"></some-components>

import SomeComponent from 'some-component'

export defaulr class App extends Vue {
  $refs = {
    myComp: SomeComponent
  }
  
  // by anonymous object
  myVar: SomeComponent = this.$refs.myComp

  // by `any` type
  myOtherVar: SomeComponent = (this.$refs as any).myComp
}
```