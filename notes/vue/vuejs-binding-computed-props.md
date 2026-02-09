# Vue Basics - Two-Way Binding, Computed and Props

## Two-Way Binding

We will begin with this:

Create a file called `TwoWayBind.vue` in your components folder.

```html
<script setup>
import { ref } from 'vue';

const number1 = ref(0)
const number2 = ref(0)
const sum = ref(0)
</script>

<template>
  <div>
    <h2>Two Way Binding Example</h2>
    <input type="number" placeholder="Enter first number">
    <input type="number" placeholder="Enter second number">
    <button >Calculate Sum</button>
    <p>Number 1: {{ number1 }}</p>
    <p>Number 2: {{ number2 }}</p>
    <p>Sum: {{ sum }}</p>
  </div>
</template>
```
