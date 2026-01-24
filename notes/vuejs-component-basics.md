# Vue.js - Creating components

## Components folder

In your project folder, open the `src` folder and add a new folder and name it `components`, if does not already exist.

## Add a new component

Add a new file and name it `BasicComponent.vue`, this will be our first component.

Copy the following code and paste it inside `BasicComponent.vue`:

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

# Adding the component to our vue project

Navigate to the `src` folder and open the `App.vue` file, this is our main entry point for the website.

Once `App.vue` is opened, you will see the `<script>` and `<template>` tag.

First we have to import our component, inside the `<script>` tag, import your component by adding this code:

```js
import BasicComponent from './components/BasicComponent.vue';
```

Once you have added the import command inside your script tag, you can now use the component in your `<template>` tag by just simply typing a tag with your component name:

```html
<BasicComponent />
```

> [!IMPORTANT]
> **Component Naming**
> Make sure the name of your component has more than one word as its description and each first letter has to be capitalized.

Congratulations! You've added your first component!
