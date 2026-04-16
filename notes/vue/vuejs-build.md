# Building your project

To set up the base and output directories in a Vue project, you primarily modify the `vite.config.js` file (for modern Vue 3 projects) or `vue.config.js` (for older Vue CLI projects).

Here is a step-by-step guide to configuring these paths.

---

## 1. Identify Your Project Tooling

Before making changes, determine if your project uses **Vite** or **Vue CLI**.

* **Vite:** Look for `vite.config.js` or `vite.config.ts`. (Standard for Vue 3).
* **Vue CLI:** Look for `vue.config.js`. (Standard for Vue 2 or early Vue 3).

---

## 2. Configuring with Vite (`vite.config.js`)

In Vite, the "base" directory handles the public path, and the "output" directory defines where the build files are saved.

### Step 1: Open `vite.config.js`

In your project root, locate and open the configuration file.

### Step 2: Set the `base` and `outDir`

Add or update the `base` and `build.outDir` properties.

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [vue()],
  
  // 1. Base Directory: The public path where your app is deployed.
  // Default is '/' (root). Use './' for relative paths or '/my-app/' for subfolders.
  base: './', 

  build: {
    // 2. Output Directory: Where the production build is generated.
    // Default is 'dist'.
    outDir: 'build_output', 
    
    // Optional: Clean the output directory before building
    emptyOutDir: true,
  }
})
```

---

## 3. Configuring with Vue CLI (`vue.config.js`)

If you are using the older Webpack-based CLI, the property names differ slightly.

### Step 1: Open `vue.config.js`

If this file doesn't exist in your root directory, create it.

### Step 2: Set `publicPath` and `outputDir`

Add the following configuration:

```javascript
const { defineConfig } = require('@vue/cli-service')

module.exports = defineConfig({
  transpileDependencies: true,

  // 1. Base Directory: Known as publicPath in Vue CLI.
  // Useful if hosting on GitHub Pages or a subdirectory.
  publicPath: process.env.NODE_ENV === 'production'
    ? '/production-subfolder/'
    : '/',

  // 2. Output Directory: Where 'npm run build' puts the files.
  outputDir: 'dist_production'
})
```

---

## 4. Summary of Key Options

| Concept | Vite Option | Vue CLI Option | Purpose |
| :--- | :--- | :--- | :--- |
| **Base Path** | `base` | `publicPath` | Adjusts the internal links in `index.html` (JS, CSS, Images) to point to the correct URL path. |
| **Output Path** | `build.outDir` | `outputDir` | Changes the name/location of the folder created after running the build command. |

---

## 5. Verify the Changes

1. **Run the Build:** Execute your build command in the terminal:

    ```bash
    npm run build
    # OR
    yarn build
    ```

2. **Check the Folder:** Look for the new directory name (e.g., `build_output`) in your project sidebar.
3. **Inspect Paths:** Open the generated `index.html` inside that folder. You should see your assets now prefixed with the path you set in the "Base" option (e.g., `<script src="./assets/index.js">`).

### Important Note on the Base Path

If you set your base path to a relative value like `./`, ensure your router is also configured to handle the base URL if you are using `createWebHistory()`.
