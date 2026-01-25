# Git workflow

## Setup and configure credentials

- Sign in VSCode with github account
- Open a new terminal inside VSCode go to your menu bar: `Terminal > New Terminal`
- Check if git is installed:

```bash
git -v
```

- Install git if not installed already (macs will already have it). At home, you can install git [for WIndows](https://git-scm.com/install/windows) and [for Mac](https://git-scm.com/install/mac).

> [!IMPORTANT]
> **Windows command fix**
> Run this in the command line if you encounter issues on windows with permission errors for git or npm:
>
> ```cmd
> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

- Once you know git is installed, add user name and email credentials for git to work:
(replace "Your Name" and use your vanier email address)

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "12345678@edu.vaniercollege.qc.ca"
```

- Set pull.rebase to true (to not write over changes)

```bash
git config --global pull.rebase true
```

## Initial commit

First class only, or whenever you want to add and upload a new repo:

Commit and Publish to github, you will have the choice of public or private repo and push.

## Commit message cannot be empty

**_MAKE SURE THERE IS A COMMIT MESSAGE BEFORE COMMITING EVERY SINGLE TIME_**

Having a message is the most critical part.

## Windows command fix

Run this in the command line if you encounter issues on windows with permission errors for git or npm:

```cmd
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
