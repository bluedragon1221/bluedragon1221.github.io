---
description: Setup a dotfiles directory using soft links
tags: tutorial
---
# Prerequisite
[[Setup Git SSH]]
# Setup
Create a new directory in your `$HOME`. Call it `dotfiles`.
```sh
mkdir ~/dotfiles
```

Initialize a Git repo in the dotfiles directory.
```sh
cd ~/dotfiles
git init
```
You can sync this repo to GitHub.

## Adding Files
Move the file into `~/dotfiles`, then create a soft link back to it's original location.
```sh
mv ~/.zshrc ~/dotfiles/
ln -sf ~/dotfiles/.zshrc ~/.zshrc
```

## Removing Files
Remove the symlink, then move it's `~/dotfiles` equivalent into it's proper place.
```sh
rm ~/.zshrc
mv ~/dotfiles/.zshrc ~/.zshrc
```

## Deploy on a New Machine
This process is called "bootstrapping".

Clone the repo, then soft link the files manually.
```sh
cd ~
git clone https://github.com/username/dotfiles
```

Then manually soft link the files to their locations.
```sh
rm ~/.zshrc
ln -sf ~/dotfiles/.zshrc ~/.zshrc
```

# Bonus
Make this process easier with a few scripts.

## Add File Function

Source this script and 
```sh
### dotfiles/manage_file.sh ###

DOT_PATH=~/dotfiles

dot_add() {
	mv $1 $DOT_PATH/
	ln -sf $DOT_PATH/$1 $1
}

dot_rm() {
	rm $1
	mv $DOT_PATH/$1 $1
}
```

## Bootstrapper Script
You can write a script to bootstrap your dotfiles automatically.
```sh
### dotfiles/bootstrapper.sh ###

# zshrc
ZSHRC_PATH=.zshrc
rm ~/$ZSHRC_PATH
ln -sf ~/dotfiles/$ZSHRC_PATH ~/$ZSHRC_PATH

# alacritty
ALACRITY_PATH=.config/alacritty/alacritty.yml

rm ~/$ALACRITTY_PATH
ln -sf ~/dotfiles/$ALACRITTY_PATH ~/$ALACRITTY_PATH
...
```
