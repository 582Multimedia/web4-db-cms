# Vue Basics - Reactivity, Declarative Rendering, Directives

## Prerequisites

We will be exploring data basics with the help of the sandbox.

Open the [Sandbox](https://sandbox.582multi.media/) in a new window.

## Reactivity and declarative rendering

### The `<script setup>` Pattern

This is the modern standard for Vue 3. It reduces boilerplate and makes the code cleaner.

`ref()`: Used to make a variable reactive.

Imports: You must explicitly import `ref` from `'vue'` inside `<script setup>`.
You only need to import `ref` once per vue file.

To change its value inside the `<script>` tag, you must use `.value`, but in the `<template>`, you access it directly.

### Template "Mustache" Syntax `{{ }}`

The most basic form of data binding is text interpolation using the "Mustache" syntax (double curly braces):

```js
<span>Message: {{ msg }}</span>
```

The mustache tag will be replaced with the value of the msg property from the corresponding component instance. It will also be updated whenever the msg property changes.

Read more about [Template Syntax](https://vuejs.org/guide/essentials/template-syntax).

### Data Types

#### Numbers

Watch out for decimal numbers

```js
0.1 + 0.2
```

#### Text

Text in double quotes

```js
"Text in double quotes"
```

Text in single quotes

```js
'Text in single quotes'
```

A full paragraph of text

```js
"Lorem ipsum, dolor sit amet consectetur adipisicing elit. Possimus quas, necessitatibus tempora non dignissimos inventore deleniti provident quibusdam, cumque vitae labore impedit numquam quasi maxime perspiciatis ipsa voluptas animi exercitationem!"
```

Multiline text

```js
`I'm on line one.
This is line two.
This is the last line.`
```

URL

```js
"https://sandbox.582multi.media/"
```

Image path

```js
"https://placehold.co/600x400?text=Sample+Image"
```

HTML text

```js
`<p>Sample Paragraph with some text. Sample text that is <em>emphasized</em>.</p>`
```

#### Boolean

Boolean value can be only `true` or `false`.

We can 'flip', or get the opposite of our value using the negation `!` symbol.

```js
!true // (not) true, will give use false
```

We can also force data to be converted into a boolean using double negative `!!` in front of the value

```js
!!0
```

```js
!!42
```

```js
!!""
```

```js
!!"some text"
```

#### conditionals

#### functions

### Directives `v-` (`bind`, `if`, `for`, `on`)

View all [Built-in Directives](https://vuejs.org/api/built-in-directives).

| Directive | Purpose | Example |
| --- | --- | --- |
| v-bind | Syncs an attribute (src, class, id) with data. | `:src="imagePath` |
| v-if | Physically adds/removes an element from the DOM. | `v-if="isLoggedIn` |
| v-for | Loops through an array to create a list. | `v-for="item in items` |
| v-on | Listens for DOM events (clicks, keyups). | `@click="submitForm` |

View examples about [Conditional Rendering](https://vuejs.org/guide/essentials/conditional).

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
