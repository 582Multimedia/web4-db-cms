# Vue.js - Starting a new project

Open a new terminal inside VSCode go to your menu bar: `Terminal > New Terminal`

## Verify if Node and npm are installed

On your first time on a computer, make sure you check if node and npm are accessible:

```bash
node -v
npm -v
```

Install [Node.js](https://nodejs.org/en) and npm if needed, or at home.

> [!IMPORTANT]
> **Windows command fix**
> Run this in the command line if you encounter issues on windows with permission errors for git or npm:
>
> ```cmd
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

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

Now, let's look at how to [run your project](vuejs-run.md).
