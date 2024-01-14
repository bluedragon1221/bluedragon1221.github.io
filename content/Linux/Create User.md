---
tags: tutorial
description: Create a new user in Linux
---
Assuming you don't want to use the root account the whole time, here's how you create a user in Linux.

# Setup `sudo`
`sudo` does not come by default on our arch installation. We need to install it and change it's configuration.
```sh
pacman -S sudo
```

Edit the `sudoers` file with this command,
```sh
EDITOR=vim visudo
```
then uncomment the line that says `:wheel ALL=(ALL) ALL`.

# ...or `doas`
[`opendoas`](https://wiki.archlinux.org/title/Doas) is the replacement for `sudo` used on openbsd. It's [more lightweight and secure](https://www.youtube.com/watch?v=brXd12LstgA) than `sudo`. First, install it:
```sh
pacman -S doas
```

Allow all users in wheel group to execute commands.
```sh
### /etc/doas.conf ###

permit persist :wheel
```

# Create User
Run this command to create a user.
```sh
useradd -mG wheel -s /bin/zsh USERNAME
```

Long-form:
```sh
useradd --create-home --gid wheel --shell /bin/zsh USERNAME
```

## Systemd-homed
An alternative to traditional user management is `systemd-homed`. To use it, you need to enable the service, then create your user.

```bash
systemctl enable --now systemd-homed
```

```bash
homectl create USERNAME --shell=/bin/zsh --uid=1000 --member-of=wheel --real-name="YOUR NAME"
```

> If you use [[Partition the Drive#BTRFS Root Partition|BTRFS for your root partition]], you can add `--storage=subvolume`, which will make your home directory a BTRFS subvolume.
# Set User Password
```sh
passwd USERNAME
```
