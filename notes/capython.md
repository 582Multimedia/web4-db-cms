# Capython Portfolio

## Requirements

Your project should have all the details enclosed inside a javascript object that you will use inside the `<script setup>` section.

**Example:**

The following is just an example json object with some fake details in it, **this is not the same as what is expected, this is only an example**.

```js
let project = {
  name: 'Fantastic Mr Capy',
  description: 'A capython movie about a capybara who loves photography and cinema.',
  version: '1.0',
  tags: ['capython', 'movie', 'photography', 'cinema', 'screenwriting'],
  images: {
    logo: "/images/logo.svg",
    storyboards: [
      "/images/storyboard-1.jpg",
      "/images/storyboard-2.jpg",
      "/images/storyboard-3.jpg",
    ],
    screenshots: [
      "/images/screenshot-1.jpg",
      "/images/screenshot-2.jpg",
      "/images/screenshot-3.jpg",
    ]
  },
  video: {
    url: 'https://www.youtube.com/watch?v=n2igjYFojUo',
    title: 'Fantastic Mr Capy - Official Trailer',
    description: 'Watch the official trailer for Fantastic Mr Capy, the capython movie of the year.',
    embed: `<iframe width="560" height="315" src="https://www.youtube.com/embed/n2igjYFojUo?si=Wv5zJhkvyKew3MQm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>`
  },
  credits: {
    director: 'Capybara Jones',
    producer: 'Capybara Jones',
    screenplay: 'Capybara Jones',
    cinematography: 'Capybara Jones',
    editing: 'Capybara Jones',
    music: 'Capybara Jones',
  },
}
```

### Details

You should include all the necessary details outlined on the [Capython page](https://github.com/582Multimedia/Multimania-Capython).

Any relevant [Capython project details](https://github.com/582Multimedia/Multimania-Capython?tab=readme-ov-file#multimania-project-details) and [Capyskills Package](https://github.com/582Multimedia/Multimania-Capython?tab=readme-ov-file#description-of-project-figma) should be included in your portfolio object.

### Images

Make sure all your images are resized and placed in the `public` folder inside your project and **not** in `src/assets`.

Make sure you organize your images inside the `images` or `img` folder as usual.

Any images included this way, should be accessible via `"/images/example.jpg"` as shown above inside the json portfoliio object.

You can then loop through the list of images like we saw in class within vue.

**Other ways to use images are much more complicated**, more details can be found here: [How to use images with Vite and Vue]((https://medium.com/@andrewmasonmedia/how-to-use-images-with-vite-and-vue-937307a150c0)).

## Start your project

> [!IMPORTANT]
> Make sure you are in your root folder inside vscode when you begin this new project.

Start a new project using

```bash
npm create vue@latest
```

Name your project **appropriately** (the name of your actual capython project would be great) or use something like `capython-portfolio` and select the options we enabled in class.

and then `cd` (change directory) command to go inside your directory and run `npm install` to install the dependancies vue needs to run, live compile and build your project. Run `npm run dev` to start the live server and work on your project.

```bash
cd <your-project-name>
npm install
npm run dev
```

## Build your project

> [!WARNING]
> Only build your project when everything is completed and ready to be built and upload on the server.

> [!CAUTION]
> Do not forget to change your `base` and `build` options inside defineConfig.

Inside `vite.config.js`, make sure you add these options for changing the path and the build output directory inside `defineConfig`.

**Example:**

```js
export default defineConfig({
  base: '/web4/example',
  build: {
    outDir: '../httpdocs/web4/example',
    emptyOutDir: true,
  },
  plugins: [vue(), vueDevTools()],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url)),
    },
  },
})
```
