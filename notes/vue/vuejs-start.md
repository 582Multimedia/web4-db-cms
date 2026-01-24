# Vue.js - Starting a new project

Open a new terminal inside VSCode go to your menu bar: `Terminal > New Terminal`

## Verify if Node and npm are installed

On your first time on a computer, make sure you check if node and npm are accessible:

```bash
node -v
npm -v
```

Install [Node.js](https://nodejs.org/en) and npm if needed, or at home.

## Start a new project

View the Vue.js [Quick Start](https://vuejs.org/guide/quick-start) guide.

```bash
npm create vue@latest
```

vue options we need:

- router
- pinia
- eslint
- prettier

View the Vue.js [Introduction](https://vuejs.org/guide/introduction) guide.

## Run your project

Make sure you are inside your project when you `cd` (change directory) into your project folder, for example, we've made a `class-exercises` folder:

```bash
cd class-exercises
```

If it is the first time you open your project (after creating your project or if you open it on a new computer), run the install command to install all the dependencies:

```bash
npm install
```

Once you have installed the dependencies, simply run `dev` to start the local server:

```bash
npm run dev
```
