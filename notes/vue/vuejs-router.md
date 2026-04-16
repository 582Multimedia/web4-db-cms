# Vue Router

## Understanding Vue Router: The Core Principles

Vue Router is the official router for Vue.js. It transforms a single-page application (SPA) from a static component into a multi-view experience by syncing the browser's URL with the displayed components.

### 1. How It Works

In a traditional multi-page website, clicking a link requests a new HTML file from the server. In a Vue SPA, the server only sends one HTML file. Vue Router intercepts the URL change and dynamically swaps components on the page without a full reload.

---

## Key Components

To implement routing, we rely on two primary functional components provided by the library:

* **`<router-link>`**: Replaces the standard `<a>` tag. It prevents the browser from reloading and allows Vue Router to handle the navigation.
* **`<router-view>`**: A functional "placeholder" component. It renders the component that matches the current URL path.

---

## Setup and Implementation

### The Router Configuration (`router/index.js`)

This file defines the "map" of your application. Each route consists of a `path` and the `component` it should load.

```javascript
import { createRouter, createWebHistory } from 'vue-router';
import HomeView from '../views/HomeView.vue';
import AboutView from '../views/AboutView.vue';

const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    component: AboutView
  }
];

const router = createRouter({
  history: createWebHistory(),
  routes
});

export default router;
```

---

## Practical Examples

### Using CSS Grid for Main Layout

When building a professional interface, it is best practice to use **CSS Grid** to define your navigation and content areas. This ensures that the `<router-view>` always sits within a consistent layout structure.

```vue
<template>
  <div class="app-layout">
    <nav class="sidebar">
      <router-link to="/">Dashboard</router-link>
      <router-link to="/about">Settings</router-link>
    </nav>

    <main class="content-area">
      <router-view />
    </main>
  </div>
</template>

<style scoped>
.app-layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  min-height: 100vh;
}

.sidebar {
  background-color: #2c3e50;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.sidebar a {
  color: white;
  text-decoration: none;
}

.content-area {
  padding: 40px;
  background-color: #f4f7f6;
}
</style>
```

### Programmatic Navigation (Composition API)

Sometimes you need to move the user to a different page after an action (like submitting a form or logging in). We use the `useRouter` hook for this.

```vue
<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const handleAction = () => {
  // Logic goes here (e.g., saving data)
  
  // Redirect to the home page
  router.push('/');
};
</script>

<template>
  <button @click="handleAction">Complete Task</button>
</template>
```

---

## Summary

1. **Define** your paths in a central router file.
2. **Mount** the router in your main application file (`main.js`).
3. **Navigate** using `<router-link>` for menus.
4. **Display** views using `<router-view>` inside a structured layout (ideally using CSS Grid).
