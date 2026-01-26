# Vue Basics - Declarative Rendering, Reactivity, Directives

## Prerequisites

We will be exploring data basics with the help of the sandbox.

Open the [Sandbox](https://sandbox.582multi.media/) in a new window.

## Data Basics

- numbers
- text
- boolean
- arrays
- objects
- array of objects
- functions
- `!=`
- `trim()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim)
- `push()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
- `pop()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
- `@keyup.enter` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/API/Element/keyup_event)
- forms - [read documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form)
- `filter()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- `every()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- `splice()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

## Mustache Syntax `{{ }}`

## Directives `v-` (`bind`, `if`, `for`, `on`)

The `<script setup>` Pattern
This is the modern standard for Vue 3. It reduces boilerplate and makes the code cleaner.

`ref()`: Used to make a variable reactive. To change its value in JavaScript, you must use .value, but in the template, you access it directly.

Imports: You must explicitly import `ref` or `computed` from `'vue'`.

| Directive | Purpose | Example |
| --- | --- | --- |
| v-bind | Syncs an attribute (src, class, id) with data. | `:src="imagePath` |
| v-if | Physically adds/removes an element from the DOM. | `v-if="isLoggedIn` |
| v-for | Loops through an array to create a list. | `v-for="item in items` |
| v-on | Listens for DOM events (clicks, keyups). | `@click="submitForm` |

```js
<script setup>
import { ref } from 'vue'

// Reactive State
const title = ref('My Morning Routine')
const tasks = ref([
  { id: 1, text: 'Brew Coffee', completed: false },
  { id: 2, text: 'Check Emails', completed: false }
])

// Logic (Functions)
const toggleTask = (task) => {
  task.completed = !task.completed
}
</script>

<template>
  <div class="container">
    <h1>{{ title }}</h1>
    
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <span :class="{ 'is-done': task.completed }">
          {{ task.text }}
        </span>
        <button @click="toggleTask(task)">
          {{ task.completed ? 'Undo' : 'Done' }}
        </button>
      </li>
    </ul>

    <p v-if="tasks.length === 0">All tasks completed!</p>
  </div>
</template>

<style scoped>
.is-done {
  text-decoration: line-through;
  color: gray;
}
</style>
```

To make the task list truly interactive, we need to capture user input. In Vue 3, we do this using the v-model directive combined with a ref from the Composition API.

## Understanding Two-Way Binding

Normally, data flow in a UI is one-way: JavaScript sends data to the HTML. Two-way binding means:

JS to HTML: If the code changes the variable, the input field updates.

HTML to JS: If the user types in the input field, the variable updates automatically.

```js
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

.value: Remember that inside the `<script setup>`, you must use newTaskText.value to access or change the data. In the `<template>`, you just use newTaskText.

Event Modifiers: Notice `@keyup.enter`. This is a Vue helper that triggers the function only when the "Enter" key is pressed, making the UX much smoother.
