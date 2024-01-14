---
description: Make your shell scripts "glamorous" with `gum`
tags: Linux, tutorial
---
# Installing
Arch:
```sh
pacman -S gum
```

Debian:
```sh
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://repo.charm.sh/apt/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/charm.gpg
echo "deb [signed-by=/etc/apt/keyrings/charm.gpg] https://repo.charm.sh/apt/ * *" | sudo tee /etc/apt/sources.list.d/charm.list
sudo apt update && sudo apt install gum
```

Fedora:
```sh
echo '[charm]
name=Charm
baseurl=https://repo.charm.sh/yum/
enabled=1
gpgcheck=1
gpgkey=https://repo.charm.sh/yum/gpg.key' | sudo tee /etc/yum.repos.d/charm.repo
sudo yum install gum
```

# Usage
## Gum `input`
This is used for quick, one line inputs.

Example:
```sh
gum input > text.txt
```

You can pass the `--placeholder` flag like so:
```sh
gum input --placeholder "type text here:" > text.txt
```

## Gum `write`
This is used for long, multi-line inputs.

Example:
```
gum write > text.txt
```

You can also use the `--placeholder` flag in the same way.

## Gum `confirm`
This gives a yes/no choice. It returns `1` on no and `0` on yes.

Example:
```sh
gum confirm "root?" && sudo -s || echo "never mind"
```

## Gum `choose`


# Flashcards
quick, one line input in gum:: `gum input`
<!--SR:!2022-12-31,15,290-->
longer, multi line input in gum:: `gun write`
<!--SR:!2022-12-25,9,250-->
yes or no in gum:: `gum confirm`
<!--SR:!2022-12-27,7,230-->
