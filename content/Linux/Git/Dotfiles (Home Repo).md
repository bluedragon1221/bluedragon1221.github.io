---
description: Setup dotfiles using a git repo in your `$HOME`
tags: tutorial
---
# Prerequisite
[[Setup Git SSH]].

# Setup
Create a repo in your `$HOME`.
```sh
cd ~
git init
```

Create a `.gitignore` file with the following contents:
```gitignore
*
```
This makes all files and directories in the git repo ignored by default.

# Usage
## Adding Files
To add a file, force `git` to bypass the `.gitignore` file:
```sh
git add -f ~/.zshrc
```

## Removing Files
To remove a file, simply make `git` forget about it.
```sh
git rm ~/.zshrc
```

## Deploy on a New Machine
In your `$HOME`, add your dotfiles repo as a remote origin. Then pull all files to your computer.
```sh
cd ~
git remote add origin git@github.com:bluedragon1221/dotfiles
git pull
```
