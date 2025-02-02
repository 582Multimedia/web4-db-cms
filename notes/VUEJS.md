# Vue.js Intro

## Start a new project

View the Vue.js [Quick Start](https://vuejs.org/guide/quick-start) guide.

```bash
npm create vue@latest
```

## Basic component example

View the Vue.js [Introduction](https://vuejs.org/guide/introduction) guide.

```vue
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

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
    <path
        d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32l0 144L48 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l144 0 0 144c0 17.7 14.3 32 32 32s32-14.3 32-32l0-144 144 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-144 0 0-144z"
    />
```

Decrement

```svg
</svg>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
    <path
        d="M432 256c0 17.7-14.3 32-32 32L48 288c-17.7 0-32-14.3-32-32s14.3-32 32-32l352 0c17.7 0 32 14.3 32 32z"
    />
</svg>
```

Reset

```svg
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
