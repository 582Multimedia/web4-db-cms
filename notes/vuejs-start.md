# Vue.js Intro

## Verify if Node and npm are installed

```bash
npm -v
node -v
```

Install [Node.js](https://nodejs.org/en) and npm if needed, or at home.

## Start a new project

View the Vue.js [Quick Start](https://vuejs.org/guide/quick-start) guide.

```bash
npm create vue@latest
```

vue options we need:

- router
- pinia
- eslint
- prettier

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
