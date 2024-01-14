---
tags: tutorial
description: Create an fstab file using `genfstab`
---
# Genfstab
## Installing
* `genftsab` is installed by default in the Arch Linux live environment.
* Once you have installed Arch Linux, it is available on the AUR.
* On other distros, it is available [here](https://github.com/glacion/genfstab)

## Usage
Generate an `fstab` with `-U`, then the mount location. `-U` uses UUIDs to identify each mount point.

```sh
genfstab -U /mnt > /mnt/etc/fstab
```

### Labels
If your partitions are labeled, you can use `-L` to use labels instead of `-U` for UUIDs. see [[Partition the Drive#Why Labels?|Why Labels?]] for more information