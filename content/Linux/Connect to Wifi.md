---
tags: tutorial
description: Connect to wifi on Linux
---
# Installation
Install `iwctl` or `networkmanager` with your distro's package manager.

# Usage
## `iwctl`
### Find SSID
Find the name of your network. If you already know this, skip this step.
```sh
iwctl station wlan0 get-networks
```

### Connect to the Network
```sh
iwctl station wlan0 connect [SSID]
```

### Password
If your network has a password, it will prompt for it.

> Note: `iwctl` doesn't play nice with captive portals, which are used when you sign into public wifi networks. If you are planning on using captive portals, use `nmcli`.

## `nmcli`
### Find SSID
Find the name of your network. If you already know this, skip this step.
```sh
nmcli device wifi
```

### Connect to the Network
```sh
nmcli device wifi connect [SSID]
```

### Password
If your network has a password, tell it to prompt for the password.
```sh
nmcli --ask dev wifi connect [SSID]
```