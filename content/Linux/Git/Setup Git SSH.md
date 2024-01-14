---
description: Setup `git` and connect it to Github via SSH
tags: tutorial
---
# Prerequisite
Install `git`.
Have a [Github](https://github.com) account.

# Set Name and Email
Give Git your name and email.
```sh
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```
This email will be public on your git commits, so you may want to use your Github noreply email, found in the settings.

## Master -> Main
Recently, Github changed the default branch name to main, but `git`'s default is still master. Use this command to switch it:
```sh
git config --global init.defaultBranch main
```

This will print you the username and email that you typed:
```sh
git config --get user.name
git config --get user.email
```

# Generate SSH Key
Create an `ssh` key if it doesn't exist.
```sh
[[ -f ~/.ssh/id_rsa.pub ]] || ssh-keygen -C $(git config --get user.email)
```

Copy your public key to the [[Linux Clipboard]].
```sh
cat ~/.ssh/id_rsa.pub | xclip -sel c
```

Paste this code in Github Settings > import SSH & GPG keys.

Verify your SSH key.
```sh
ssh -T git@github.com
```
