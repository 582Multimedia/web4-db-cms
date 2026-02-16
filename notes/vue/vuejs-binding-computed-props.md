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

To make the task list truly interactive, we need to capture user input. In Vue 3, we do this using the v-model directive combined with a ref from the Composition API.

## Understanding Two-Way Binding

Normally, data flow in a UI is one-way: JavaScript sends data to the HTML. Two-way binding means:

JS to HTML: If the code changes the variable, the input field updates.

HTML to JS: If the user types in the input field, the variable updates automatically.

```html
<script setup>
import { ref } from 'vue'

const tasks = ref([
  { id: 1, text: 'Brew Coffee', completed: false }
])

// 1. Create a ref to track the new task input
const newTaskText = ref('')

const addTask = () => {
  // Prevent adding empty tasks
  if (newTaskText.value.trim() === '') return

  // 2. Push new object to the array
  tasks.value.push({
    id: Date.now(), // Simple unique ID
    text: newTaskText.value,
    completed: false
  })

  // 3. Clear the input field
  newTaskText.value = ''
}

const toggleTask = (task) => {
  task.completed = !task.completed
}
</script>

<template>
  <div class="app-container">
    <h2>Task Manager</h2>

    <div class="input-group">
      <input 
        v-model="newTaskText" 
        @keyup.enter="addTask"
        placeholder="What needs to be done?"
      />
      <button @click="addTask">Add Task</button>
    </div>

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <span :class="{ 'is-done': task.completed }">{{ task.text }}</span>
        <button @click="toggleTask(task)">Check</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.is-done { text-decoration: line-through; color: #888; }
.input-group { margin-bottom: 20px; }
</style>
```

Key Takeaways for this Step
v-model: This is your "bridge." It links the `<input>` value directly to newTaskText.

`.value`: Remember that inside the `<script setup>`, you must use newTaskText.value to access or change the data. In the `<template>`, you just use newTaskText.

Event Modifiers: Notice `@keyup.enter`. This is a Vue helper that triggers the function only when the "Enter" key is pressed, making the UX much smoother.

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
