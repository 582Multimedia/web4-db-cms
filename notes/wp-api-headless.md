# Wordpress API

First make sure you have installed wordpress on your server. If you need to see how to install wordpress, click here.

## Wordpress API / Headless Wordpress

In order for us to by pass wordpress theme system and use the data from our site directly through the wordpress API, we have to enable just one setting.

In the `Dashboard`, under `Settings`, **select** `Permalinks`.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.40 AM.jpg>)

The permalinks setting will appear.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.50 AM.jpg>)

Under the list of options in permalink structure, **select** the `Post name` option.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.53 AM.jpg>)

Go to the bottom of the page and **click** on `Save Changes`.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.55 AM.jpg>)

You have now enabled the wordpress javascript API!

To view your wordpress installation's API, you can go to this path:

< wordpress path >/wp-json/wp/v2

where < wordpress path > is the path on your server for wordpress.

For my example, you can visit the following paths:

**API base path (display all the paths):**
[https://ngy.582mi.com/headless/wp-json/wp/v2](https://ngy.582mi.com/headless/wp-json/wp/v2)

**Posts path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/posts](https://ngy.582mi.com/headless/wp-json/wp/v2/posts)

**Pages path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/pages](https://ngy.582mi.com/headless/wp-json/wp/v2/pages)

## Integrating wordpress API inside vue

Create a new component called `WpApiTest.vue`.

```js
<script setup>
import { onMounted, ref } from "vue";
let wordpress = ref([]);
let fetchData = async () => {
  try {
    const response = await fetch("https://ngy.582mi.com/headless/wp-json/wp/v2/posts");
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    wordpress.value = data;
  } catch (error) {
    console.error(error);
  }
};
onMounted(() => {
  fetchData();
});
</script>

<template>
  <div>
    <h1>WP API Test</h1>
    <ul>
      <li v-for="item in wordpress" :key="item.id">
        {{ item }}
      </li>
    </ul>
  </div>
</template>
```

Import and insert the component tag into your App.vue to see what you can do with it.

## Custom Post Types

We can access custom post types and taxonomies via the names we defined.

In our example:

**Movies path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/movies](https://ngy.582mi.com/headless/wp-json/wp/v2/movies)

**Genres path:**
[https://ngy.582mi.com/headless/wp-json/wp/v2/genre](https://ngy.582mi.com/headless/wp-json/wp/v2/genre)

Make new components and integrate these paths into some custom components!
