# Vue.js - Run your project

Open a new terminal inside VSCode go to your menu bar: `Terminal > New Terminal`

Make sure you are inside your project when you `cd` (change directory) into your project folder, for example, we've made a `class-exercises` folder:

```bash
cd class-exercises
```

If it is the first time you open your project (after creating your project or if you open it on a new computer), run the install command to install all the dependencies:

```bash
npm install
```

> [!IMPORTANT]
> **Windows command fix**
> Run this in the command line if you encounter issues on windows with permission errors for git or npm:
>
> ```cmd
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

Once you have installed the dependencies, simply run `dev` to start the local server:

```bash
npm run dev
```

> [!NOTE]
> [Install the Vue (Official) extension](https://marketplace.visualstudio.com/items?itemName=Vue.volar) if you did not already.

Your project is now running! Let's look at how to [create our first component](vuejs-component-basics.md).
