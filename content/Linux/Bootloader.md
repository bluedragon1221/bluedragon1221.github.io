---
tags:
  - tutorial
description: Install a bootloader on your linux installation
---

`systemd-boot` is the ultimate bootloader for Linux. It boots your system, and nothing else.

> [!note]
> This only works for [[Partition the Drive#Check for UEFI]|UEFI Systems]]
## Install the Bootloader
Ideally, `bootctl` should be able to automatically detect your `EFI` partition.
```sh
bootctl install
```

If it doesn't find it, then you can use `cfdisk`.
1. Open your drive with `cfdisk`
2. Select the drive that you want to be your `EFI` system partition
3. Select `[ Type ]`
4. Select `EFI System`
5. Select `[ Write ]`, and type `yes`
6. Select `[ Quit ]`

If all else fails, you can use `--esp-path=/efi` to force it to install to the right location.

## Unified Kernel Image
While `systemd-boot` technically supports loading an initrd, I still perfer to use a Unified Kernel Image. `systemd-boot` has first class suport for UKIs and will detect them automatically.

We'll build our UKI with `mkinitcpio`.
### Kernel Command Line
Normally, you would put your kernel command line in your `GRUB_CMDLINE...`, but you don't have that anymore. `mkinitcpio` looks for kernel cmdline files in `/etc/cmdline.d/*`

It is required to specify a `root` parameter, at least. For example, if you are using labels and btrfs, this might be your cmdline.
```sh
## /etc/cmdline.d/root.conf

root=LABEL=root rootflags=subvol=@ rw rootfstype=btrfs
```

### Preset File
`mkinitcio` uses two files to build your initramfs. `/etc/mkinitcpio.conf`, and `/etc/mkinitcpio.d/linux.preset`. We'll edit the latter one to tell `mkinitcpio` to bundle the microcode, kernel, and initramfs into a unified kernel image.
```diff
# mkinitcpio preset file for the 'linux' package

- ALL_config="/etc/mkinitcpio.conf"
ALL_kver="/boot/vmlinuz-linux"
ALL_microcode=(/boot/*-ucode.img)

PRESETS=('default', 'fallback')

- default_config="/etc/mkinitcpio.conf"
- default_image="/boot/initramfs-linux.img"
+ default_uki="/efi/EFI/Linux/arch-linux.efi"
+ default_options="--splash /usr/share/systemd/bootctl/splash-arch.bmp"

- fallback_config="/etc/mkinitcpio.conf"
- fallback_image="/boot/initramfs-linux-fallback.img"
+ fallback_uki="/efi/EFI/Linux/arch-linux-fallback.efi"
+ fallback_options="-S autodetect"
```
Be sure to replace `/efi` with where your EFI system partition is mounted.

### Installing
Actually, `systemd-boot`automatically looks for Unified Kernel Images in `/efi/EFI/Linux`, so we don't have to do anything to install it.
## Extension
https://www.reddit.com/r/archlinux/comments/qy281v/boot_an_archlinux_iso_directly_from_my_boot_using/