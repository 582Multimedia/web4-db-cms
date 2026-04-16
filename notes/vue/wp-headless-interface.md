# Interfacing with the WordPress REST API

Interfacing with the WordPress REST API to manage Custom Post Types (CPTs) requires a specific configuration on the WordPress side before you can send requests. By default, custom post types are often hidden from the API.

This guide assumes you have a CPT already registered (e.g., `book`, `service`, or `portfolio`).

---

## 1. Enable API Support for your CPT

For a Custom Post Type to appear in the REST API, it must be registered with specific arguments.

<!-- If you are using a plugin like **CPT UI**, ensure "Show in REST API" is set to **True**.

If you are using code in `functions.php`, ensure your `register_post_type` call includes these keys:

```php
$args = array(
    'public'        => true,
    'show_in_rest'  => true, // CRITICAL: Enables the REST API
    'rest_base'     => 'books', // Optional: The URL slug (defaults to post type name)
    'supports'      => array('title', 'editor', 'custom-fields', 'author'),
    // ... other args
);
register_post_type('book', $args);
```

### Exposing Custom Fields (Meta)

To add data to custom fields via the API, you must also register the meta keys:

```php
register_meta('post', 'book_isbn', array(
    'show_in_rest' => true,
    'single'       => true,
    'type'         => 'string',
));
```
 -->

---

## 2. Set Up Authentication

You cannot "POST" (create) items anonymously. The easiest modern method is **Application Passwords** (introduced in WP 5.6).

1. Log into your WP Admin.
2. Go to **Users > Profile**.
3. Scroll to **Application Passwords**.
4. Enter a name (e.g., "External App") and click **Add New Application Password**.
5. **Copy the password.** You won't see it again.

---

## 3. Identify the Endpoint

The standard endpoint for a CPT follows this pattern:
`https://your-site.com/wp-json/wp/v2/<rest_base>`

* **Default:** `https://example.com/wp-json/wp/v2/book`
* **With Custom Rest Base:** `https://example.com/wp-json/wp/v2/books`

---

## 4. Make the REST Request

You must send a **POST** request with **Basic Auth** (using your username and the Application Password) and a **JSON** body.

### Example using cURL

```bash
curl -X POST https://example.com/wp-json/wp/v2/books \
    -u "your_username:your_application_password" \
    -H "Content-Type: application/json" \
    -d '{
        "title": "The Great Gatsby",
        "content": "A story about the American dream.",
        "status": "publish",
        "meta": {
            "book_isbn": "978-0743273565"
        }
    }'
```

### Example using JavaScript (Fetch)

```javascript
const postData = {
    title: 'New Book Title',
    content: 'Description of the book goes here...',
    status: 'publish', // Use 'draft' if you don't want it live immediately
    meta: {
        book_isbn: '123456789'
    }
};

const username = 'admin';
const appPassword = 'xxxx xxxx xxxx xxxx xxxx';

fetch('https://example.com/wp-json/wp/v2/books', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Basic ' + btoa(`${username}:${appPassword}`)
    },
    body: JSON.stringify(postData)
})
.then(response => response.json())
.then(data => console.log('Success:', data))
.catch(error => console.error('Error:', error));
```

---

## Troubleshooting Checklist

* **401 Unauthorized:** Check your Application Password and ensure your user has "Edit Posts" capabilities for that CPT.
* **404 Not Found:** Verify `show_in_rest` is true. Try flushing your permalinks (**Settings > Permalinks > Save Changes**).
* **Meta not saving:** Ensure you used `register_meta` with `'show_in_rest' => true`. If you use **Advanced Custom Fields (ACF)**, enable the "Show in REST API" toggle in the Field Group settings.

To interface a **Vue.js** frontend with a **WordPress REST API** using **Custom Post Types (CPT)** and **Advanced Custom Fields (ACF)**, follow this consolidated workflow.

Since you are using **Advanced Custom Fields (ACF)**, the process is much more streamlined. ACF has built-in support for the REST API, so you don't necessarily need to manually write `register_meta` functions in PHP.

Here is the updated guide to interfacing with WordPress using ACF.

---

## 1. Enable REST API in ACF Settings

For your custom fields to be accessible via the API, you must toggle the REST settings within the ACF UI:

1. Navigate to **ACF > Field Groups**.
2. Edit your specific Field Group.
3. Click on the **Settings** tab (usually at the top or bottom of the group editor).
4. Ensure **Show in REST API** is toggled **ON**.
5. *(Optional)* You can change the **REST API Namespace** if you want them grouped under a specific key, but the default is `acf`.

---

## 2. Verify CPT "REST" Support

Even with ACF enabled, the Post Type itself must be visible to the API.

* Go to **ACF > Post Types** (if you created the CPT through ACF).
* Under the **General** or **Advanced** settings, ensure **Show in REST API** is enabled.

---

## 3. The REST API Payload Structure

When using ACF, the data structure in your JSON body changes. Instead of placing custom fields inside a `meta` object, ACF expects them inside an **`acf`** object.

### The Request Format

* **Method:** `POST`
* **Endpoint:** `https://example.com/wp-json/wp/v2/books`
* **Body Structure:**

```json
{
    "title": "The Great Gatsby",
    "content": "A classic novel.",
    "status": "publish",
    "acf": {
        "book_isbn": "978-0743273565",
        "author_name": "F. Scott Fitzgerald",
        "genre": "Fiction"
    }
}
```

---

## 4. Implementation Example (Node.js/JavaScript)

Here is how you would programmatically send that data using the Fetch API:

```javascript
async function createBookWithACF() {
    const url = 'https://example.com/wp-json/wp/v2/books';
    const credentials = btoa('username:xxxx xxxx xxxx xxxx'); // Your App Password

    const payload = {
        title: 'The Catcher in the Rye',
        status: 'publish',
        // ACF data goes here
        acf: {
            'book_isbn': '978-0316769488',
            'publication_year': 1951
        }
    };

    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Authorization': `Basic ${credentials}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(payload)
    });

    const result = await response.json();
    console.log(result);
}
```

---

## Important ACF Considerations

### Field Names vs. Field Keys

By default, ACF allows you to use the **Field Name** (e.g., `book_isbn`) in the REST API. However, if you find that values aren't saving correctly, you can try using the **Field Key** (e.g., `field_65af1234abcd`) as the key in your JSON object.

### Handling Different Field Types

* **Images/Files:** You must first upload the media to the `/wp/v2/media` endpoint, get the **ID**, and then pass that ID integer into the ACF field.
* **Select/Radio:** Send the `value` of the choice.
* **Relationship/Post Object:** Send an array of IDs, e.g., `[123, 456]`.

### Troubleshooting ACF API

If the `acf` field does not appear in your API response when you perform a `GET` request, double-check that the **ACF plugin is active** on the site and the "Show in REST API" toggle is definitely saved for that specific field group

---

## 1. WordPress Configuration

Before writing code, ensure WordPress is configured to "talk" to your application.

### Custom Post Type (CPT)

Whether using code or a plugin (like CPT UI), the post type must have:

* **Show in REST API:** `True`
* **REST API base:** (e.g., `books`)

### Advanced Custom Fields (ACF)

1. **Show in REST API:** Enable this toggle in the **Field Group Settings**.
2. **Field Names:** Note your "slugs" (e.g., `isbn_number`), as these are the keys used in your JSON.

### Authentication

1. Navigate to **Users > Profile**.
2. Generate an **Application Password**.
3. Store this securely; it is required for all `POST` requests.

---

## 2. Data Architecture

The WordPress API expects a specific JSON structure. Standard fields (Title, Content) sit at the root, while ACF fields must be nested inside an `acf` object.

| Field Type | JSON Key | Placement |
| :--- | :--- | :--- |
| **Title** | `title` | Root level |
| **Content** | `content` | Root level |
| **Status** | `status` | Root level (`publish`, `draft`, `pending`) |
| **ACF Fields** | `acf` | **Nested object** |

---

## 3. Vue.js Implementation

This component manages the state, handles the encoding of credentials, and performs the asynchronous request.

### The Component (`AddBook.vue`)

```vue
<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="form.title" placeholder="Book Title" required />
    <textarea v-model="form.content" placeholder="Description"></textarea>

    <input v-model="form.acf.isbn_number" placeholder="ISBN" />
    <select v-model="form.acf.genre">
      <option value="fiction">Fiction</option>
      <option value="history">History</option>
    </select>

    <button :disabled="isSending">Submit</button>
  </form>
</template>

<script setup>
import { reactive, ref } from 'vue';

const isSending = ref(false);

const form = reactive({
  title: '',
  content: '',
  status: 'publish',
  acf: {
    isbn_number: '',
    genre: 'fiction'
  }
});

const handleSubmit = async () => {
  isSending.value = true;
  
  // Base64 encode credentials: "username:application-password"
  const auth = btoa('admin_user:xxxx xxxx xxxx xxxx');

  try {
    const response = await fetch('https://your-site.com/wp-json/wp/v2/books', {
      method: 'POST',
      headers: {
        'Authorization': `Basic ${auth}`,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(form)
    });

    if (response.ok) alert('Item added successfully!');
  } catch (err) {
    console.error('API Error:', err);
  } finally {
    isSending.value = false;
  }
};
</script>
```

---

## 4. Common Pitfalls & Tips

* **CORS Issues:** If your Vue app is on `localhost` and WP is on `website.com`, install the **"JSON Basic Auth"** plugin or add `Access-Control-Allow-Origin` headers to your WordPress `.htaccess`.
* **Security:** Never hardcode Application Passwords in a production frontend. Use environment variables or, ideally, a **Backend Proxy** (Nuxt Server Routes or a simple Node/Express bridge) to hide the credentials.
* **Validation:** If an ACF field is marked "Required" in WordPress, the API request **will fail** if that field is missing from the `acf` object.
* **Media:** To upload images via ACF, you must first POST to `/wp/v2/media`, get the attachment **ID**, and send that ID as the value for your ACF image field.
