# Vue.js Intro

Open a new terminal inside VSCode go to your menu bar: `Terminal > New Terminal`

## Verify if Node and npm are installed

On your first time on a computer, make sure you check if node and npm are accessible:

```bash
node -v
npm -v
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

## Run your project

Make sure you are inside your project when you `cd` (change directory) into your project folder, for example, we've made a `class-exercises` folder:

```bash
cd class-exercises
```

If it is the first time you open your project (after creating your project or if you open it on a new computer), run the install command to install all the dependencies:

```bash
npm install
```

Once you have installed the dependencies, simply run `dev` to start the local server:

```bash
npm run dev
```

## Basic component example

View the vue essentials components basics guide [here](https://vuejs.org/guide/essentials/component-basics).

### Creating a new component

#### Components folder

In your project folder, open the `src` folder and add a new folder and name it `components`, if does not already exist.

#### Add a new component

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

### Adding the component to our vue project

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
