# Temp notes - to be used later

<!-- ```js
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
``` -->

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

- `@keyup.enter` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/API/Element/keyup_event)
- arrays
- objects
- array of objects
- `trim()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim)
- `push()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
- `pop()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
- forms - [read documentation](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form)
- `filter()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- `every()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- `splice()` - [read documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

Imports: You must explicitly import `ref` or `computed` from `'vue'`.

## Computed Properties

Integrating Computed Properties is where the "logic" of your Vue application becomes truly efficient.

In the Composition API, a `computed` property is a reactive variable that derives its value from other reactive state (like our `tasks` array). The best part? It is **cached** — it only re-calculates when its dependencies change.

Derived State & Filtering

1. Tracking Statistics
Instead of manually updating a counter every time a task is added or checked, we let Vue calculate it automatically.

2. Dynamic Filtering
We can create a "filtered" version of our list without actually deleting data from the original array. This allows the user to toggle between "All," "Active," and "Completed" views.

The "Enhanced" Task Manager
Here is the implementation using the Composition API. We’ll add a "Filter" state and two computed properties.

```html
<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { id: 1, text: 'Brew Coffee', completed: true },
  { id: 2, text: 'Learn Computed Properties', completed: false }
])

const newTaskText = ref('')
const currentFilter = ref('all') // 'all', 'active', or 'completed'

// --- Computed Properties ---

// 1. Calculate remaining tasks automatically
const remainingCount = computed(() => {
  return tasks.value.filter(t => !t.completed).length
})

// 2. Filter the list based on user selection
const filteredTasks = computed(() => {
  if (currentFilter.value === 'active') {
    return tasks.value.filter(t => !t.completed)
  } else if (currentFilter.value === 'completed') {
    return tasks.value.filter(t => t.completed)
  }
  return tasks.value
})

// --- Methods ---
const addTask = () => {
  if (!newTaskText.value.trim()) return
  tasks.value.push({ id: Date.now(), text: newTaskText.value, completed: false })
  newTaskText.value = ''
}
</script>

<template>
  <div class="app">
    <h2>Task Manager</h2>
    
    <input v-model="newTaskText" @keyup.enter="addTask" placeholder="New task..." />
    
    <div class="filters">
      <button @click="currentFilter = 'all'">All</button>
      <button @click="currentFilter = 'active'">Active</button>
      <button @click="currentFilter = 'completed'">Completed</button>
    </div>

    <p>Items left: <strong>{{ remainingCount }}</strong></p>

    <ul>
      <li v-for="task in filteredTasks" :key="task.id">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ done: task.completed }">{{ task.text }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done { text-decoration: line-through; opacity: 0.6; }
.filters { margin: 10px 0; display: flex; gap: 5px; }
button { cursor: pointer; }
</style>
```

Why use computed instead of a method?

| Feature | `computed(() => ...)` | `methodName()` |
| -- | -- | -- |
| Execution | Runs only when a dependency changes. | Runs every time the component re-renders. |
| Performance | High (cached). | Lower (re-calculates every time). |
| Usage | Used like a variable: `{{ remainingCount }}`. | Called like a function: `{{ getCount() }}`. |
  
## Components

The Component Breakdown
We will split our "Task Manager" into a parent container and three specialized children:

- `App.vue` (The Parent): Holds the "Source of Truth" (the tasks array) and the logic.
- `TaskInput.vue`: Just a text box and a button.
- `TaskItem.vue`: A single row in our list.
- `TaskStats.vue`: A small footer showing the counts.

1. The Child: `TaskInput.vue` (Emitting Events)
This component doesn't know about the `tasks` array. It only knows how to grab a string and "shout" it up to the parent.

```html
<script setup>
import { ref } from 'vue'

// Define the "events" this component can send to the parent
const emit = defineEmits(['add-task'])
const newTask = ref('')

const submit = () => {
  if (newTask.value.trim()) {
    emit('add-task', newTask.value) // Sending the data up
    newTask.value = ''
  }
}
</script>

<template>
  <div class="input-row">
    <input v-model="newTask" @keyup.enter="submit" placeholder="Add a task..." />
    <button @click="submit">Add</button>
  </div>
</template>
```

2. The Child: TaskItem.vue (Receiving Props)
This component receives a single task object as a Prop. It tells the parent when a user wants to delete or toggle it.

```html
<script setup>
// Define the "data" this component expects from the parent
const props = defineProps(['task'])
const emit = defineEmits(['toggle', 'delete'])
</script>

<template>
  <li>
    <input type="checkbox" :checked="props.task.completed" @change="emit('toggle')" />
    <span :class="{ done: props.task.completed }">{{ props.task.text }}</span>
    <button @click="emit('delete')">×</button>
  </li>
</template>
```

3. The Parent: App.vue (The Orchestrator)
This is where we import the children and manage the state.

```html
<script setup>
import { ref } from 'vue'
import TaskInput from './components/TaskInput.vue'
import TaskItem from './components/TaskItem.vue'

const tasks = ref([{ id: 1, text: 'Learn Props & Emits', completed: false }])

const handleAdd = (text) => {
  tasks.value.push({ id: Date.now(), text, completed: false })
}

const removeTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id)
}
</script>

<template>
  <div class="app">
    <h1>My Project</h1>
    
    <TaskInput @add-task="handleAdd" />

    <ul>
      <TaskItem 
        v-for="task in tasks" 
        :key="task.id" 
        :task="task" 
        @toggle="task.completed = !task.completed"
        @delete="removeTask(task.id)"
      />
    </ul>
  </div>
</template>
```

Why this matters

Reusability: You can use TaskInput.vue in a different part of your app without rewriting code.

Testing: It's much easier to test a small component than a 500-line file.

Collaboration: One developer can work on the styling of TaskItem while another works on the logic in App.vue.

## Props

https://vuejs.org/guide/components/props
