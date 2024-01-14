---
tags: tutorial
description: Setup pipewire to enable audio
---
# Installation
Install the following packages,
```sh
sudo pacman -S pipewire wireplumber wireplumber
```

enable services,
```sh
systemctl --user enable wireplumber
```

And reboot.
```sh
reboot
```

## Change Volume
with `wireplumber`, you can change the volume with `wpctl`.

```sh
# Decrease volume
wpctl set-volume @DEFAULT_AUDIO_SINK@ -5%

# Increase volume
wpctl set-volume @DEFAULT_AUDIO_SINK@ +5%

# Set volume
wpctl set-volume @DEFAULT_AUDIO_SINK@ 20%
```