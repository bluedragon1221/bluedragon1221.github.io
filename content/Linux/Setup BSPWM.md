---
tags: tutorial
description: How to setup the best WM ever
---
[BSPWM](https://github.com/baskerville/bspwm) stands for Binary Space Partitioning Window Manager, referring to its window splitting scheme.

# Installation
Install X server.
```sh
sudo pacman -S xorg-server xorg-xinit
```

Install `bspwm`,`sxhkd`, a terminal emulator, and any other tools you use.
```sh
sudo pacman -S bspwm sxhkd alacritty
```

# Basic Configuration
## Window Manager
Since `bspwm` doesn't have a configuration file by default, we need to give it one. We can copy the default one to `~/.config/bspwm/bspwmrc`. Since this location changes per distro, we can just use the find command, then copy that file to the right location.

```sh
find / -name bspwmrc

mkdir ~/.config/bspwm
cp {FILE FROM ABOVE} ~/.config/bspwm/bspwmrc
```

## Keyboard Shortcuts
If we just start `bspwm` with that configuration, it will be unusable. We won't be able to control it. Enter `sxhkd`, the **S**imple **X**11 **H**ot**K**ey **D**aemon made by the creator of `bspwm`.

We'll make a file at `~/.config/sxhkd/sxhkdrc`. Edit the file with the following:
```sxhkdrc
super + enter
 alacritty
```

Now at least we can start a terminal!

## `.xinitrc`
The way we start all of these programs is the `~/.xinitrc` file. This file will run with the command `startx`. Create `~/.xinitrc`, and edit it with the following:
```sh
exec bspwm
```

Now run `startx`, and watch the magic! if you press `super` + `enter`, a full screen `alacritty` window will open.