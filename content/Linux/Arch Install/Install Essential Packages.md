# Install Essential Packages
The base of Arch Linux is installed using the pacstrap command. This will take a long time depending on your internet connection, so your should probably [[Update Mirrors with Reflector|update your mirrors]] first.

## Update Keyring
Depending on how outdated your Arch Linux ISO is, you may need to force update the `archlinux-keyring` before you `pacstrap`.

> Note: Normally, partial updates are a bad idea, but it doesn't really matter if you break the Arch Linux installation environment

```sh
pacman -Sy archlinux-keyring
```

## Run `pacstrap`
Pacstrap will install the base packages to your system
```sh
pacstrap /mnt base linux linux-firmware
```

You can add any other packages to this command. I generally add my text editor of choice, networking tools, and grub as well.
```sh
pacstrap /mnt base linux linux-firmware \
              vim zsh \
              networkmanager \
```

