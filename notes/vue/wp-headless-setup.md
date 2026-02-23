# Wordpress API

First make sure you have installed wordpress on your server. If you need to see how to install wordpress, [click here](https://youtube.com/playlist?list=PLe6HRxcu-AsDN4fspmBf-CtLCNLYE_ZHr&si=fHv0sixY27yA-qWe).

You should already have a wordpress installed from Bruce's class, it should be located at your web2 page, something like:

`https://peter00.582something.com`/cms/

**Replace** `https://peter00.582something.com` **with your site link**.

To login and access the dashboard / wordpress admin, go to:

`https://peter00.582something.com`/cms/**wp-admin**

## Wordpress API / Headless Wordpress

In order for us to skip wordpress theme system and use the data from our site directly through the wordpress API, we have to enable just one setting.

In the `Dashboard`, under `Settings`, **select** `Permalinks`.

![alt text](</img/wp-headless/Screenshot 2025-04-06 at 11.18.40 AM.jpg>)

The permalinks setting will appear.

![alt text](</img/wp-headless/Screenshot 2025-04-06 at 11.18.50 AM.jpg>)

Under the list of options in permalink structure, **select** the `Post name` option.

![alt text](</img/wp-headless/Screenshot 2025-04-06 at 11.18.53 AM.jpg>)

Go to the bottom of the page and **click** on `Save Changes`.

![alt text](</img/wp-headless/Screenshot 2025-04-06 at 11.18.55 AM.jpg>)

You have now enabled the wordpress javascript API!

To view your wordpress installation's API, you can go to this path:

`your-wordpress-path/` wp-json/wp/v2

where `your-wordpress-path/` is the path on your server for the wordpress you are working on.

For my example, you can visit the following paths:

**API base path (display all the paths):**
[https://ngy.582mi.com/headless/wp-json/wp/v2](https://ngy.582mi.com/headless/wp-json/wp/v2)

**Posts path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/posts](https://ngy.582mi.com/headless/wp-json/wp/v2/posts)

**Pages path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/pages](https://ngy.582mi.com/headless/wp-json/wp/v2/pages)

## Integrating wordpress API inside vue

Create a new component called `WpApiBasics.vue` and add the following code:

```js
<script setup>
import { ref, onMounted } from 'vue';

// ### Initialize state with null or empty values

const posts = ref([]);
const isLoading = ref(true);
const errorMessage = ref('');

// 2. Define the asynchronous fetch function
const fetchPosts = async () => {
  try {
    const response = await fetch('https://ngy.582mi.com/headless/wp-json/wp/v2/posts');
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
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
      <li v-for="post in posts" :key="post.id">
        <p>{{ post }}</p>
      </li>
    </ul>
  </div>
</template>

```

Import and insert the component tag into your `App.vue` to see what you can do with it.

Once it works with my data, make your own component and use the same code, but **replace the link with your wordpress API**.

Make sure you use your own path for `posts` (`wp-json/wp/v2/posts`) or `pages` (`wp-json/wp/v2/pages`) and **not** the root path at `wp-json/wp/v2/`.

![alt text](</img/wp-headless/Screenshot 2026-02-23 at 2.11.04 PM.jpg>)

To view the incoming object from wordpress in your browser, open the link. You can expand the object by checking the `Pretty-print` button.

![alt text](</img/wp-headless/Screenshot_2026-02-23_at_10.41.32_AM.png>)

![alt text](</img/wp-headless/Screenshot_2026-02-23_at_10.41.38_AM.png>)

Modify the code in your component to make it prettier!

For example, to display the title of your post / page, you can change the default `post` variable to get the title inside, using `post.title.rendered` by looking at the object you're getting from wordpress (see above).

![alt text](</img/wp-headless/Screenshot 2026-02-23 at 2.14.05 PM.jpg>)

![alt text](</img/wp-headless/Screenshot 2026-02-23 at 2.13.17 PM.jpg>)

Choose some other information from the objects and display them in your component (ex: the `id`)!

Once this is done, move on to [adding custom post types in wordpress](/notes/vue/wp-headless-custom-post-type.md).
