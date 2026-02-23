# 📝 Vue API Integration: The Essentials

This course plan is designed to take students from "hardcoded data" to "dynamic, production-ready API integration." Since they already understand props and reactivity, we’ll focus on the **lifecycle**, **asynchronous state**, and **clean architecture**.

## Real-World Data Fetching in Vue 3

Duration: 4 Modules (Approx. 4–6 hours of instruction)

### Module 1: The Lifecycle & The `fetch` API

Before we can load data, we need to know when to ask for it.

- The `onMounted` Hook: Understanding why we don't fetch data in the global scope (avoiding SSR issues and ensuring the DOM is ready).

- The Anatomy of a Fetch: Using the native Fetch API with `async`/`await`.

- Reactive State: Initializing refs with `null` or empty arrays to prevent undefined errors during the first render.

### Module 2: Handling the "In-Between" States

Users hate a blank screen. We’ll learn to manage the three pillars of any API call.

- Loading States: Creating a `const isLoading = ref(false)` toggle.

- Error Handling: Using `try...catch` blocks to capture 404s or network failures.

- Empty States: Handling the `"No results found"` scenario gracefully.

### Module 3: Component Architecture & Props

Now we connect their existing knowledge of Props to the API layer.

- Smart vs. Dumb Components: * Parent: Fetches the data from the API.

  - Child: Receives the data via `props` and renders it.

- The "Key" Prop: Using unique IDs from the API to optimize the `v-for` directive.

- Conditional Rendering: Using `v-if` and `v-else` to switch between a loading spinner and the data list.

### Module 4: Abstraction with Composables

To keep components clean, we’ll move the logic into reusable functions.

- The `useFetch` Pattern: Creating a custom Composable to encapsulate the loading and error logic.

- Axios vs. Fetch: A brief comparison and why you might choose a library for interceptors and automatic JSON parsing.

- Final Project: Build a "GitHub Profile Finder" or a "Movie Search App" that reacts to user input.

Technical Concept: The Data Flow

Since students know two-way binding, it’s important to show how the API flow differs:

| Step | Action | Vue Mechanism |
| --- | --- | --- |
| 1 | Component Mounts | `onMounted()` |
| 2 | Trigger Request | `async`/`await` `fetch()` |
| 3 | Update State | `data.value = response` |
| 4 | UI Reacts | `v-for` & `{{ moustache }}` |

**Instructor's Note**: Remind students that while `v-model` (two-way binding) is great for forms, API data is usually a **one-way flow**—from the server to the state, and then down to the child components via props.

## Module 1

Here is a clean template for Module ### This example uses the **Composition API**
(Script Setup) and **JSONPlaceholder**, a free fake API, to demonstrate the core logic of fetching data and handling the initial reactive state.

## Module 1 Starter: The `onMounted` Fetch

This template focuses on the sequence: **Initialize → Mount → Fetch → Update**.

`App.vue`

```html
<script setup>
import { ref, onMounted } from 'vue';

// ### Initialize state with null or empty values

const posts = ref([]);
const isLoading = ref(true);
const errorMessage = ref('');

// 2. Define the asynchronous fetch function
const fetchPosts = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5');
    
    if (!response.ok) {
      throw new Error('Failed to fetch data');
    }
    
    // Update our reactive ref with the data
    posts.value = await response.json();
  } catch (err) {
    errorMessage.value = err.message;
  } finally {
    // Stop the loading indicator regardless of success or failure
    isLoading.value = false;
  }
};

// 3. Trigger the fetch when the component is added to the DOM
onMounted(() => {
  fetchPosts();
});
</script>

<template>
  <div class="container">
    <h1>Latest Posts</h1>

    <div v-if="isLoading" class="loading">
      Retrieving posts...
    </div>

    <div v-else-if="errorMessage" class="error">
      Error: {{ errorMessage }}
    </div>

    <ul v-else>
      <li v-for="post in posts" :key="post.id" class="post-card">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.post-card {
  border: 1px solid #ddd;
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 8px;
  list-style: none;
}
.error { color: red; font-weight: bold; }
.loading { font-style: italic; color: #666; }
</style>
```

### Key Discussion Points for Students

Why `ref([])`? If we didn't initialize `posts` as an array, the `v-for` would throw an error on the first render before the API responds.

The `try`/`catch`/`finally` Pattern:

- `try`: The "Happy Path."
- `catch`: The "Safety Net."
- `finally`: The "Cleanup" (turning off the loading spinner).

**The Network Tab**: Show students how to open Chrome DevTools to see the actual XHR request happening in real-time.

## Module 2 Notes: Handling the "In-Between" States

In this module, we move beyond just fetching data. We focus on the **User Experience (UX)**. In the real world, APIs take time to respond, and sometimes they fail. Your app must handle these "in-between" states gracefully.

### **The Three Pillars of API State**

To create a professional interface, you must track three specific reactive variables:

- `data`: The actual information from the server (initialized as `null` or `[]`).

- `isLoading`: A boolean to track if the request is in progress (starts as `false` or `true`).

- `error`: A place to store an error message if the "Happy Path" fails.

### **The Professional Pattern**: `try...catch...finally`

This is the "Golden Standard" for writing asynchronous functions in Vue. It ensures your app doesn't crash and that the UI always updates.

- `try`: Run your fetch logic here. If it works, save the data.

- `catch`: If anything goes wrong (network down, 404), this block catches the error so you can display it to the user.

- `finally`: This block runs no matter what. This is the perfect place to set `isLoading.value = false`.

### **Template Logic**: `v-if`, `v-else-if`, and `v-else`

Your HTML template should act like a switchboard based on your state variables:

- **If Loading**: Show a spinner or a skeleton screen.

- **Else if Error**: Show an alert box with the error message.

- **Else**: Show the actual data list.

### **Common Pitfall: The "Fetch 404" Trap**

**Crucial Note**: The native `fetch()` API only "fails" (goes to the `catch` block) if there is a network error (like being offline). If the server returns a `404 Not Found` or `500 Server Error`, `fetch()` still thinks it succeeded!

The Fix: You must manually check `if (!response.ok)` and `throw` an error yourself to trigger the `catch` block.

💡 **Module 2 Summary Checklist**

- [ ] Did I create a ref for isLoading?
- [ ] Did I wrap my fetch in a try/catch block?
- [ ] Did I use finally to turn off the loading indicator?
- [ ] Does my template use v-if to hide the data while loading?

This "Code Along" script is designed for a live demonstration. You can start with a broken, "silent" app and gradually add the UX layers so students see exactly why each piece of code is necessary.

### Live Demo Script: **The "Resilient Fetch"**

#### **Step 1: The "Silent" Fetch (The Starting Point)**

- Goal: Show why we need more than just a `ref` for data.

- Code: Write a basic fetch that only sets `data.value`.

- Action: Toggle your browser to "Slow 3G" in the Network tab.

- Observation: Point out that the screen is completely blank for 5 seconds. The user has no idea if the app is working or crashed.

#### **Step 2: Adding the "Pulse" (Loading State)**

- Goal: Give the user visual feedback.

- Code: Add `const isLoading = ref(false)`.

- Logic: Set it to `true` at the start of the function and `false` at the end.

- Template: Add a `<div v-if="isLoading">`.

- Observation: Now the user sees "Loading..." immediately. The app feels "alive."

#### **Step 3: Simulating the Crash (Error Handling)**

- Goal: Handle the "Unchecked Promise" error.

- Action: Change the API URL to something that doesn't exist (e.g., .../posts-wrong).

- Code: Wrap the logic in try { ... } catch (err) { ... }.

- The "Manual Throw": Show them that fetch doesn't catch a 404 automatically.

    ```js
    if (!response.ok) throw new Error("Server said no! (404)");
    ```

- Observation: Instead of a console error that users never see, we now show a helpful message on the screen.

#### **Step 4: The Safety Net (The finally Block)**

- Goal: Ensure the UI doesn't get "stuck."

- Action: Show what happens if an error occurs but you forgot to set isLoading.value = false in the catch. The spinner spins forever!

- Code: Move the toggle to a finally block.

    ```js
    finally {
    isLoading.value = false;
    }
    ```

- Observation: Success or failure, the spinner stops. The app is ready for the user's next move.

#### 🛠️ **Discussion Questions to Ask the Class**

1. **"What happens if the user's internet is disconnected halfway through?"** (Tests
their understanding of the `catch` block).
2. **"Why don't we just use a 'success' boolean instead of 'isLoading'?"** (Leads to a discussion about state-driven UI).
3. **"Where should the 'finally' block go if we want to reset a form after a POST request?"** (Prepares them for future CRUD operations).

### Module 2 Student Lab Task

**Task**: Take your "User List" from Module 1 and:

1. Add a **CSS Spinner** (or a simple "Loading..." text).
2. Add a **"Simulate Error" button** that changes the URL to an invalid one to test the error UI.
3. Ensure the loading message disappears even if the API fails.

## Module 3

In **Module 3**, we move from "everything in one file" to a professional architecture. We separate the **Logic (Smart Component)** from the **UI (Dumb Component)**.

This is a crucial moment for students because it proves why they learned props: to pass API data down the component tree.

**The "Smart" Parent**: `PostList.vue`
The Parent's job is to manage the lifecycle, the `fetch` call, and the loading state. It doesn't care how the posts look; it just cares about getting them.

```html
<script setup>
import { ref, onMounted } from 'vue';
import PostItem from './PostItem.vue'; // Importing the Child

const posts = ref([]);
const isLoading = ref(true);

const loadData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=3');
    posts.value = await res.json();
  } finally {
    isLoading.value = false;
  }
};

onMounted(loadData);
</script>

<template>
  <section>
    <h2>Community Feed</h2>

    <p v-if="isLoading">Loading feed...</p>
    
    <div v-else class="feed-grid">
      <PostItem 
        v-for="post in posts" 
        :key="post.id" 
        :post-data="post" 
      />
    </div>
  </section>
</template>
```

**The "Dumb" Child**: `PostItem.vue`
The Child's job is purely presentational. It receives data via `props` and renders it. It has no idea an API even exists.

```html
<script setup>
// Defining the prop to receive the post object
const props = defineProps({
  postData: {
    type: Object,
    required: true
  }
});
</script>

<template>
  <article class="card">
    <h3>{{ postData.title }}</h3>
    <p>{{ postData.body }}</p>
    <button @click="$emit('read-more', postData.id)">Read Full Post</button>
  </article>
</template>

<style scoped>
.card {
  border-left: 4px solid #42b883;
  padding: 1rem;
  background: #f9f9f9;
  margin: 0.5rem 0;
}
h3 { text-transform: capitalize; color: #2c3e50; }
</style>
```

### Why This Matters (The "Prop Drilling" Lesson)

By splitting these, you teach students two professional standards:

- **Reusability**: You can use `PostItem.vue` anywhere (search results, favorites, etc.) without rewriting the API logic.

- **Testability**: You can test the UI of `PostItem` by just passing in "fake" data via props without needing a working internet connection.

### Student Exercise

Ask the students to add a "Delete" button in the Child component that emits an event back to the Parent to remove that specific post from the `posts` array. This combines their knowledge of **props (down)** and **emits (up)** with **API state**.

## Module 4

In **Module 4**, we reach the "Pro" level of Vue development. We’re going to take the logic from Module 1 (loading, errors, and fetching) and extract it into a **Composable**.

Think of a Composable as a "logic sandwich" that any component can take a bite of. This keeps our components incredibly thin and focused only on the template.

### **The Composable**: `useFetch.js`

We create a separate file (usually in a `/composables` folder). This function manages its own internal reactive state and returns it to the component.

```js
import { ref, watchEffect } from 'vue';

export function useFetch(url) {
  const data = ref(null);
  const error = ref(null);
  const loading = ref(true);

  const fetchData = async () => {
    loading.value = true;
    error.value = null; // Reset error on new attempts
    
    try {
      const res = await fetch(url);
      if (!res.ok) throw new Error('Could not fetch the data');
      data.value = await res.json();
    } catch (err) {
      error.value = err.message;
    } finally {
      loading.value = false;
    }
  };

  // Run immediately, and re-run if the URL changes
  fetchData();

  return { data, error, loading };
}
```

### **The Refactored Parent**: `PostList.vue`

Look how much cleaner the component becomes. We no longer need `onMounted` or complex `try`/`catch` blocks here because the Composable handles the heavy lifting.

```html
<script setup>
import { useFetch } from './composables/useFetch';
import PostItem from './PostItem.vue';

// All the logic is now a single line!
const { data: posts, error, loading } = useFetch('https://jsonplaceholder.typicode.com/posts?_limit=3');
</script>

<template>
  <div>
    <div v-if="loading" class="spinner">🌀 Loading...</div>
    
    <div v-else-if="error" class="alert-error">
      {{ error }}
    </div>

    <div v-else>
      <PostItem v-for="p in posts" :key="p.id" :post-data="p" />
    </div>
  </div>
</template>
```

### The Architecture Shift

Why this is a "Game Changer" for Students:

- **Dry Code (Don't Repeat Yourself)**: If they need to fetch users in another component, they just call `useFetch('/users')`. They don't have to rewrite the loading/error logic.

- **Readability**: The component now reads like a story: "I am using fetch for this URL, and here is how I display the results."

- **Reactivity**: Because the Composable returns **Refs**, the UI will still update automatically when the data arrives.

### Project Idea: The Searchable API

To wrap up the course, challenge the students to:

1. Create an input field with `v-model`.
2. Pass that search term into a URL (e.g., `https://api.github.com/users/${username}`).
3. Watch the Composable automatically re-fetch data whenever the user types.

To ensure students can effectively debug their work, here is a **Troubleshooting Cheat Sheet** and a **Grading Rubric** to evaluate their final API projects.

### **🛠️ The "Why Isn't It Loading?" Cheat Sheet**

Students often hit the same three walls. Distributing this as a handout will save you hours of individual troubleshooting.

| Error/Symptom | The Likely Culprit | The Fix |
| --- | --- | --- |
| CORS Error (in Console) | Security restriction by the API server. | Use a public API (like JSONPlaceholder) or a proxy. Explain that localhost is often blocked by private APIs. |
| v-for is blank | Initial state is null or the array is nested. | Check if the API returns an object or an array. Use `console.log(data.value)` to inspect the shape. |
| "Uncaught in Promise" | A 404 or 500 error from the server. | Ensure the `fetch` logic includes `if (!res.ok) throw new Error()`. |
| Infinite Loading | The `loading.value` never gets set to `false`. | Move `loading.value = false` into a `finally` block so it runs regardless of success/error. |

### 📝 Project Grading Rubric

Project Goal: Build a "GitHub User Search" or "Movie Database" using a Composable.

| Criteria | 1: Novice | 2: Proficient | 3: Master |
| --- | --- | --- | --- |
| State Management | Hardcoded data or no loading indicator. | Uses `ref` for data and a basic `loading` toggle. | Manages `data`, `loading`, and `error` states perfectly. |
| Architecture | All logic is in one massive component. | Logic is split into Parent/Child components via props. | Logic is fully extracted into a reusable `useFetch` Composable. |
| UX / UI | App crashes on invalid search or bad API response. | Displays a basic "Error" message. | Gracefully handles Empty, Loading, and Error states with UI feedback. |
| Clean Code | Uses `var`, no comments, messy formatting. | Uses `const`/`let` and follows Vue 3 style guide. | Semantic naming, clean `async`/`await` syntax, and proper prop validation. |

### Final "Pro Tip" for the Instructor

When students start using `v-model` for search inputs, they will accidentally trigger **hundreds of API** calls while typing. This is the perfect "teaching moment" to introduce **Debouncing**—delaying the API call until the user stops typing for 500ms.

To handle a search input without crashing the API (or your rate limit), we introduce **Debouncing**. This ensures the API is only called once the user has stopped typing for a set amount of time (e.g., 500ms).

Here is how to upgrade the `useFetch` composable to handle dynamic, debounced search terms.

### **The Debounced Composable**: `useDebouncedFetch.js`

We use a `watch` function to observe a reactive `searchQuery`. Instead of fetching immediately, we start a timer. If the user types again, we clear the old timer and start a new one.

```js
import { ref, watch } from 'vue';

export function useDebouncedFetch(baseUrl, queryRef) {
  const data = ref(null);
  const loading = ref(false);
  const error = ref(null);
  let timeout = null;

  const fetchData = async (query) => {
    if (!query) {
      data.value = null;
      return;
    }

    loading.value = true;
    try {
      const res = await fetch(`${baseUrl}${query}`);
      if (!res.ok) throw new Error('Search failed');
      data.value = await res.json();
    } catch (err) {
      error.value = err.message;
    } finally {
      loading.value = false;
    }
  };

  // Watch the search query and debounce the API call
  watch(queryRef, (newQuery) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => {
      fetchData(newQuery);
    }, 500); // 500ms delay
  });

  return { data, loading, error };
}
```

### **The Implementation**: `SearchView.vue`

Now, the component just passes a `ref` to the composable. The "magic" happens behind the scenes.

```html
<script setup>
import { ref } from 'vue';
import { useDebouncedFetch } from './composables/useDebouncedFetch';

const searchTerm = ref('');
// We pass the reactive 'searchTerm' directly into the composable
const { data: results, loading } = useDebouncedFetch(
  'https://api.github.com/search/repositories?q=', 
  searchTerm
);
</script>

<template>
  <div class="search-container">
    <input 
      v-model="searchTerm" 
      placeholder="Search GitHub Repos..." 
      class="search-input"
    />

    <div v-if="loading" class="loader">Searching...</div>
    
    <ul v-else-if="results">
      <li v-for="repo in results.items" :key="repo.id">
        {{ repo.full_name }}
      </li>
    </ul>
  </div>
</template>
```

### 💡 Key Lessons for Students

- **Performance**: Explain that without debouncing, typing "Javascript" (10 letters) triggers 10 separate network requests. With debouncing, it triggers **one**.

- **The "Clean Up" Concept**: `clearTimeout` is essential. If you don't clear the previous timer, you'll still get a "waterfall" of 10 requests, just delayed by 500ms.

- **UX Pattern**: Mention that this is how Google Search and Amazon’s search bar work in the real world.

### Project Delivery

At this point, your students have built:

1. A **Reactive UI** that handles loading/error states.
2. A **Component Architecture** using Props.
3. A **Reusable Logic Layer** with Composables.
4. A **Performance Optimization** with Debouncing.

### Quiz

Here is a retention quiz to test your understanding of API loading, Vue components, and the use of Composables for data fetching.

[Vue 3 API Integration Mastery](<https://gemini.google.com/share/448a41c6a9b4>)

## Summary 📝 Vue API Integration: The Essentials

### The Lifecycle (`onMounted`)

The Rule: Never fetch data in the "naked" script tag. Use `onMounted`.

Why? It ensures the component is actually in the browser before you try to update state or interact with the DOM.

State Prep: Always initialize your ref with the correct type (e.g., `ref([])` for lists) so the template doesn't crash while waiting for data.

### The Three States of Loading

Every API call needs a "User Experience" plan for three scenarios:

Loading: Use a boolean (`isLoading = true`) to show a spinner or "Loading..." text.

Success: The `try` block where you save the data to your reactive variable.

Error: The `catch` block where you save the error message to show the user what went wrong.

### Component Architecture (Props)

Smart (Parent): The "Brain." It fetches the data and holds the master state.

Dumb (Child): The "Face." It receives data via props and looks pretty.

The Key: Always use a unique ID (like `post.id`) for the `:key` in a `v-for`. It helps Vue update the list efficiently.

### Composables (The `useFetch` Pattern)

Definition: Moving your `fetch`, `loading`, and `error` logic into a separate `.js` file.

Benefits: Makes your code DRY (Don't Repeat Yourself). You can reuse the same fetching logic across 10 different components.

Return Values: A composable must `return { data, loading, error }` so the component can use them.

### Performance (Debouncing)

The Problem: Without it, every single keystroke in a search bar triggers a new, expensive API request.

The Solution: Use a `setTimeout` to wait until the user stops typing (usually 500ms).

The Cleanup: You must use `clearTimeout` to cancel the previous timer before starting a new one, or you'll get a "waterfall" of delayed requests.

### 🚀 Student Pro-Tips

Inspect it: Use the **Network Tab** in Chrome DevTools to see the actual JSON data coming back.

Check "ok": Native `fetch` doesn't fail on 404s. Always check `if (!response.ok)` manually.

Safety First: Use `v-if="data"` in your template to ensure you don't try to render properties of `null`.

Would you like me to create a "Code Challenge" list based on these notes for the students to complete?

To turn those notes into action, here is a set of Level-Up Challenges. These are designed to be completed in order, with each one adding a new layer of complexity to their API skills.

## 🛠️ The Vue API Challenge List

### Level 1: The Basics (The "Fetch & Show")

**Goal**: Successfully connect to a public API and display data.

- **Task**: Use onMounted to fetch a list of 10 users from `https://jsonplaceholder.typicode.com/users` .

- **Requirement**: Display just the `name` and `email` of each user in a simple `<ul>`.

- **Bonus**: Add a "Refresh" button that triggers the fetch function again manually.

### Level 2: The UX Specialist (States & Errors)

**Goal**: Prevent the "flash of empty content" and handle failures.

- **Task**: Add a `v-if`/`v-else` structure to your Level 1 project.

- **Requirement**: Show a loading spinner (or text) while the data is fetching.

- **Requirement**: Intentionally break the URL (e.g., change it to `/users-wrong`) and display a `"Something went wrong!"` message on the screen.

### Level 3: The Architect (Smart & Dumb)

**Goal**: Clean up the code by separating logic from presentation.

- **Task**: Move the code that displays the user's name and email into a child component called `UserCard.vue`.

- **Requirement**: The parent component must pass the user object to the child via `props`.

- **Requirement**: Use a CSS grid in the parent to display the `UserCard` components in a clean layout.

### Level 4: The Performance Pro (Debounce & Search)

**Goal**: Create a real-time search interface that doesn't spam the network.

- **Task**: Create a search input that filters a list of Pokémon using the PokeAPI (`https://pokeapi.co/api/v2/pokemon/`).

- **Requirement**: Implement a **debounce** so the API is only called 500ms after the user stops typing.

- **Requirement**: Use the **Network Tab** in DevTools to prove that typing "Pikachu" only sent one request, not seven.

#### Level 5: The Master (The Composable)

**Goal**: Abstract your logic so it can be used anywhere.

- **Task**: Create a `useFetch.js` file.

- **Requirement**: Move all the `try`/`catch`, `loading`, and `error` logic into this file.

- **Requirement**: Use this Composable in two different components (e.g., one for `Users` and one for `Posts`).

### 🎓 Success Checklist for Students

Before submitting, students should check:

- [ ] Did I use `const` and `ref` correctly?
- [ ] Is my `loading` state set to `false` in a `finally` block?
- [ ] Does every item in my `v-for` have a unique `:key`?
- [ ] Is my API logic separated from my HTML as much as possible?

## Module 5

Moving into **Module 5**, we shift from just reading data to interacting with it. This is where students learn the "Write" part of **CRUD** (Create, Read, Update, Delete).

In Vue, the challenge isn't just sending the request; it’s updating the local UI so the user sees the change immediately without a page refresh.

Module 5: Mutating Data (POST & DELETE)

### Sending Data (`POST`)

When a student submits a form, we need to send that object to the server.

- **The Method**: Change `fetch` method to `POST`.

- **The Body**: Use `JSON.stringify(payload)` to turn a JavaScript object into a string the server understands.

- **The Headers**: You must tell the server you are sending JSON by setting `'Content-Type': 'application/json'`.

### Deleting Data (`DELETE`)

Deleting is usually simpler because we only need the **ID** of the item.

- **The URL**: Usually looks like `https://api.com/posts/1`.

- **The Local Update**: After a successful delete on the server, we must remove it from our reactive posts array using .filter().

💻 **Code Example: The "Action" Component**
Here is how you would handle adding a new post and deleting an existing one in a single component.

```html
<script setup>
import { ref } from 'vue';

const posts = ref([]);
const newPostTitle = ref('');

// CREATE: Adding a post
const addPost = async () => {
  const payload = { title: newPostTitle.value, body: 'New content', userId: 1 };

  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts', {
      method: 'POST',
      body: JSON.stringify(payload),
      headers: { 'Content-type': 'application/json' }
    });
    const savedPost = await res.json();
    
    // UI Update: Add the new post to the TOP of the list
    posts.value.unshift(savedPost);
    newPostTitle.value = ''; // Clear input
  } catch (err) {
    console.error("Failed to add post", err);
  }
};

// DELETE: Removing a post
const deletePost = async (id) => {
  try {
    await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`, {
      method: 'DELETE'
    });
    
    // UI Update: Remove the item locally so it disappears from the screen
    posts.value = posts.value.filter(post => post.id !== id);
  } catch (err) {
    alert("Could not delete item");
  }
};
</script>
```

### **Key Concept: "Optimistic" vs. "Pessimistic" UI**

This is a great high-level concept to teach students:

- **Pessimistic (The Code Above)**: We wait for the server to say "Success" before we change the UI. (Safer, but feels slower).

- **Optimistic**: We remove the item from the screen immediately and then send the request. If the request fails, we put the item back and show an error. (Feels instant, but harder to code).

💡 **Module 5 Summary Notes for Students**

- **Method Matters**: Default is `GET`. You must specify `method: 'POST'` or `method: 'DELETE'`.

- **Syncing the UI**: The server and your Vue `ref` are two different things. If you delete on the server but forget to `.filter()` your array, the item stays on the screen!

- **Headers**: Don't forget `'Content-Type': 'application/json'` or the server might ignore your data.

🎓 **Final Lab Challenge**

**The "Mini-Blog" Manager**:

### Use your `useFetch` composable to load a list of posts

1. Add a simple text input and "Add" button to create a new post.
2. Add a "🗑️" button next to every post that deletes it from the list.
