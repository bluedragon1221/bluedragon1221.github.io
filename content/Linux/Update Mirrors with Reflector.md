In Arch Linux, mirrors are not automatically changed based on your location. Instead, Arch users use [`reflector`](https://wiki.archlinux.org/title/Reflector) to update mirrors.

# Update Mirrors
## Backup
Make a backup of the `mirrorlist` file before doing this, as it will overwrite the current one.
```sh
cp /etc/pacman.d/mirrorlist /ect/pacman.d/mirrorlist.bak
```

## Run `reflector`
```sh
reflector --protocol https \
          --latest 10 \
          --sort rate \
          --save /etc/pacman.d/mirrorlist
```
