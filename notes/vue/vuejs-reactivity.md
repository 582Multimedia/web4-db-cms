# Vue Basics - Reactivity, Declarative Rendering, Directives

## Prerequisites

We will be exploring data basics with the help of the sandbox.

Open the [Sandbox](https://sandbox.582multi.media/) in a new window.

## Reactivity and declarative rendering

### The `<script setup>` Pattern

This is the modern standard for Vue 3. It reduces boilerplate and makes the code cleaner.

`ref()`: Used to make a variable reactive.

```js
const msg = ref("Hello world!")
```

Imports: You must explicitly import `ref` from `'vue'` inside `<script setup>`.
You only need to import `ref` once per vue file.

To change its value inside the `<script>` tag, you must use `.value`, but in the `<template>`, you access it directly.

### Template "Mustache" Syntax `{{ }}`

The most basic form of data binding is text interpolation using the "Mustache" syntax (double curly braces):

```html
<span>Message: {{ msg }}</span>
```

The mustache tag will be replaced with the value of the msg property from the corresponding component instance. It will also be updated whenever the msg property changes.

Read more about [Template Syntax](https://vuejs.org/guide/essentials/template-syntax).

### Data Types

#### Numbers

Whole numbers are called integers, which is considered a Number.

```js
const basicInteger = ref(1)
```

Decimal numbers are called floats, but is a Number in javascript.

```js
const basicDecimal = ref(0.1)
```

We can also use expressions inside our declaration.

```js
const specialDecimal = ref(0.1 + 0.2)
```

Watch out for decimal numbers math...

#### Text

Text in double quotes

```js
const sampleDqText = ref("Text in double quotes")
```

Text in single quotes

```js
const sampleSqText = ref('Text in single quotes')
```

A full paragraph of text

```js
const sampleParagraphText = ref("Lorem ipsum, dolor sit amet consectetur adipisicing elit. Possimus quas, necessitatibus tempora non dignissimos inventore deleniti provident quibusdam, cumque vitae labore impedit numquam quasi maxime perspiciatis ipsa voluptas animi exercitationem!")
```

Multiline text

```js
const sampleMultilineText = ref(`I'm on line one.
This is line two.
This is the last line.`)
```

URL

```js
const sampleUrl = ref("https://sandbox.582multi.media/")
```

Image path

```js
const sampleImageUrl = ref("https://placehold.co/600x400?text=Sample+Image")
```

HTML text

```js
const sampleHtml = ref(`<p>Sample Paragraph with some text. Sample text that is <em>emphasized</em>. Sample text that is <strong>strongly emphasized</strong>.</p>`)
```

#### Boolean

Boolean value can be only `true` or `false`.

```js
const sampleBoolean = ref(true)
```

We can 'flip', or get the opposite of our value using the negation `!` symbol.

```js
const sampleNegativeBoolean = ref(!true) // (not) true, will give use false
```

We can also force data to be converted into a boolean using double negative `!!` in front of the value

```js
const sampleZeroConversion = ref(!!0)
```

```js
const sampleNonZeroConversion = ref(!!42)
```

```js
const sampleEmptyStringConversion = ref(!!"")
```

```js
const sampleNonEmptyStringConversion = ref(!!"Hello")
```

## Directives `v-` (`bind`, `if`, `for`, `on`)

View all [Built-in Directives](https://vuejs.org/api/built-in-directives).

| Directive | Purpose | Example |
| --- | --- | --- |
| v-bind | Syncs an attribute (src, class, id) with data. | `:src="imagePath` |
| v-html | Renders raw HTML inside an element. | `v-html="rawHtmlContent` |
| v-if | Physically adds/removes an element from the DOM. | `v-if="isLoggedIn` |
| v-else-if | Adds an else-if condition to a v-if block. | `v-else-if="hasPermission` |
| v-else | Adds an else condition to a v-if block. | `v-else` |
| v-show | Toggles an element's visibility via CSS. | `v-show="isVisible` |
| v-on | Listens for DOM events (clicks, keyups). | `@click="submitForm` |
| v-for | Loops through an array to create a list. | `v-for="item in items` |
| v-model | Creates two-way data binding on form inputs. | `v-model="username` |

### Binding basic data

```html
<img :src="sampleImageUrl" alt="Sample Image" />
```

### HTML binding

```html
<div v-html="sampleHtml"></div>
```

### Conditional Rendering

There are two way to use conditional rendering.

First is to generate the DOM (html) using `v-if` **only** if the condition is `true`.

```html
<section v-if="sampleBoolean">
  <p>Boolean value is true!</p>
</section>
<section v-else>
  <p>Boolean value is false!</p>
</section>
```

The other way is to generate the DOM (html) and only show / hide it using css with `v-show`.

```html
<section v-show="sampleBoolean">
  <p>This section is always in the DOM but visibility is toggled via CSS.</p>
</section>
```

View examples about [Conditional Rendering](https://vuejs.org/guide/essentials/conditional).

### Functions

We can declare functions the same way we declare variables, but using the [arrow function operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

If we do not need to feed a value for the change, we can simply use `()` as the parameter list.

```js
const toogleBoolean = () => {
  sampleBoolean.value = !sampleBoolean.value
}
```

However, if we need to pass in a value (like a new number), we can declare a parameter for the function.

```js
const setNumber = (newNumber) => {
  basicInteger.value = newNumber
}
```

### Event listeners - `v-on` (shorthand `@`)

We can add event listeners to HTML elements using the `v-on` directive (shorthand `@`).

```html
<button @click="toogleBoolean">Toggle Boolean</button>
```

Similarly, we can use the changeNumber function with a click event or an input event.:

```html
<button @click="setNumber(42)">Set Number to 42</button>
<input type="number" @input="setNumber($event.target.value)" />
```

## Arrays

An array is a special type of object that can hold multiple values in an ordered list.

```js
const arraySample = ref([1, 2, 3, 4, 5])
```

```js
const fruits = ref(['Apple', 'Banana', 'Cherry'])
```

We can loop through an array using the `v-for` directive.

```html
<ul>
  <li v-for="item in arraySample" :key="item">{{ item }}</li>
</ul>
```

```html
<ul>
  <li v-for="fruit in fruits" :key="fruit">{{ fruit }}</li>
</ul>
```

We can also loop through all the values of a number.

```html
<ul>
  <li v-for="digit in basicInteger" :key="digit">{{ digit }}</li>
</ul>
```

We can also loop through text to get each character.

```html
<ul>
  <li v-for="char in sampleDqText" :key="char">{{ char }}</li>
</ul>
```

## Objects

An object is a data structure that holds key-value pairs.

```js
const sampleObject = ref({
  name: 'John Doe',
  age: 30,
  occupation: 'Developer'
})
```

We can access object properties using dot notation.

```html
<section v-if="sampleObject">
  <p>Name: {{ sampleObject.name }}</p>
  <p>Age: {{ sampleObject.age }}</p>
  <p>Occupation: {{ sampleObject.occupation }}</p>
</section>
```

## Array of Objects

An array of objects is an array where each element is an object.

```js
const tasks = ref([
  { id: 1, text: 'Brew Coffee', completed: false },
  { id: 2, text: 'Make Breakfast', completed: true },
  { id: 3, text: 'Read News', completed: false }
])
```

We can loop through an array of objects using `v-for`.

```html
<ul>
  <li v-for="task in tasks" :key="task.id">
    <span>{{ task.id }}</span>
    <span :class="{ 'is-done': task.completed }">{{ task.text }}</span>
    <button @click="toggleTask(task)">Check</button>
    <button @click="removeTask(task)">Delete</button>
  </li>
</ul>
```
