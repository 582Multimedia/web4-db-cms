# Vue.js Intro

## Install Node and npm

[Node.js](https://nodejs.org/en)

## Start a new project

View the Vue.js [Quick Start](https://vuejs.org/guide/quick-start) guide.

```bash
npm create vue@latest
```

View the Vue.js [Introduction](https://vuejs.org/guide/introduction) guide.

## Basic component example

<https://vuejs.org/guide/essentials/component-basics>

```js
<script setup>
import { ref } from "vue";
let count = ref(0);
</script>

<template>
  <div>
    <h1>Count is: {{ count }}</h1>
    <button @click="count++">Increment</button>
  </div>
</template>

<style scoped>
/* styling goes here */
</style>
```

## Svg replacements

Increment

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
  <path
    d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32l0 144L48 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l144 0 0 144c0 17.7 14.3 32 32 32s32-14.3 32-32l0-144 144 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-144 0 0-144z"
  />
</svg>
```

Decrement

```html
</svg>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
    <path
        d="M432 256c0 17.7-14.3 32-32 32L48 288c-17.7 0-32-14.3-32-32s14.3-32 32-32l352 0c17.7 0 32 14.3 32 32z"
    />
</svg>
```

Reset

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
  <path
    d="M256 48a208 208 0 1 1 0 416 208 208 0 1 1 0-416zm0 464A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM175 175c-9.4 9.4-9.4 24.6 0 33.9l47 47-47 47c-9.4 9.4-9.4 24.6 0 33.9s24.6 9.4 33.9 0l47-47 47 47c9.4 9.4 24.6 9.4 33.9 0s9.4-24.6 0-33.9l-47-47 47-47c9.4-9.4 9.4-24.6 0-33.9s-24.6-9.4-33.9 0l-47 47-47-47c-9.4-9.4-24.6-9.4-33.9 0z"
  />
</svg>
```

CSS

```css
button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  margin: 0 0.5rem;
  padding: 0;

  svg {
    width: 2rem;
    height: 2rem;
    fill: slategray;
  }

  :hover {
    fill: white;
  }
}
```

## Integrating APIs

```js
import { onMounted, ref } from "vue";
let users = ref([]);
let fetchData = async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    users.value = data;
  } catch (error) {
    console.error(error);
  }
};
onMounted(() => {
  fetchData();
});
```

```html
<div>
  <ul>
    <li v-for="user in users" :key="user.id">
      {{ user.name }}
      <ul>
        <li>{{ user.email }}</li>
        <li>{{ user.phone }}</li>
        <li>{{ user.website }}</li>
      </ul>
    </li>
  </ul>
</div>
```

## Props

<https://vuejs.org/guide/components/props>

Create a component named `PropsExample.vue` and copy paste this inside:

```js
<!-- PropsExample.vue -->
<script setup>
const props = defineProps(['name'])
</script>
<template>
  <p>{{ name }}</p>
</template>
```

In `App.vue`, copy paste this inside the `script` tag to import the component:

```js
import PropsExample from './components/PropsExample.vue'
```

External props passed to the component in the parent using:

```js
<PropsExample name="Test Name" />
```

## Component v-model

<https://vuejs.org/guide/components/v-model.html>

Create a component named `VmodelExample.vue` and copy paste this inside:

```js
<!-- VmodelExample.vue -->
<script setup>
const number = defineModel()

function update() {
  number.value++
}
</script>

<template>
  <div>Parent bound v-model is: {{ number }}</div>
  <button @click="update">Increment</button>
</template>
```

In `App.vue`, copy paste this inside the `script` tag to import the component:

```js
import VmodelExample from './components/VmodelExample.vue'
```

The parent can then bind a value with `v-model`:

```js
<!-- Parent.vue -->
<VmodelExample v-model="countModel" />
```

## Advanced Example

We will use this object for a more intergrated example:

```js
let books = ref([
  {
    title: 'Hamlet', author: 'William Shakespeare', year: 1603, genre: 'Tragedy', excerpt: 'To be, or not to be: that is the question.'
  },
  {
    title: 'The Great Gatsby', author: 'F. Scott Fitzgerald', year: 1925, genre: 'Novel', excerpt: 'So we beat on, boats against the current, borne back ceaselessly into the past.'
  },
  {
    title: 'Moby-Dick', author: 'Herman Melville', year: 1851, genre: 'Novel', excerpt: 'Call me Ishmael.'

  },
  {
    title: 'Pride and Prejudice', author: 'Jane Austen', year: 1813, genre: 'Novel', excerpt: 'It is a truth universally acknowledged, that a single man in possession of a good fortune, must be in want of a wife.'
  },
])
```
