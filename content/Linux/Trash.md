---
tags: tutorial
description: Setup a trashcan and never loose another file
---
Recently, I deleted my whole notes directory and had to restore from a backup. In an attempt to never to this again, I created a trash system.

# Setup
Create a directory that will serve as your trashcan.
```sh
mkdir ~/.local/trash
```

Create a bash function that will override the default `rm` command.
```sh
### ~/.zshrc ###
rm() {
	mv $1 ~/.local/trash/
}
```

TODO: `rm -rf` override
