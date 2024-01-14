---
tags: tutorial
description: Get the most out of your Z Shell
---
I love `zsh`. It takes everything that bash does, and makes it 10x better; including customization.

# Installation
Install `zsh`
Since I [[Frameworks|don't use frameworks]], this tutorial will use vanilla `zsh`.

# Prompt
`zsh` completely fixes the bash `PS1` variable using prompt expansions. Since the default `zsh` prompt kind of sucks, lets make it better.

Place this in your `~/.zshrc` and reload `zsh`.
```sh
### ~/.zshrc ###
...
PROMPT="%~ %% "
...
```

Using more prompt expansions, this is my `zsh` prompt.
```sh
### ~/.zshrc ###
PROMPT="%F{blue}%~%f %B%(?.%F{green}.%F{red})%f%b "
```

[Here's a list](https://zsh.sourceforge.io/Doc/Release/Prompt-Expansion.html) of all prompt expansions.

If this level of customization isn't enough, I'd checkout [starship](https://starship.rs).

# Plugins
## Syntax Highlighting
`zsh-syntax-highlighting` colors invalid commands red and underlines valid paths.

### Installation
Clone the `zsh-syntax-highlighting` git repo.
```sh
mkdir ~/.config/zsh; cd ~/.config/zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting
```

Source the repo at the end of your `~/.zshrc`.
```sh
### ~/.zshrc ###
...
source ~/.config/zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

For more info on installing `zsh-syntax-highlighting`, see [here](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md).

## Auto Suggestions
`zsh-autosuggestions` predicts what you are about to type based on your history.

### Installation
The installation is essentially the same as [[#Syntax Highlighting]].

Clone the git repo,
```sh
cd ~/.config/zsh
git clone https://github.com/zsh-users/zsh-autosuggestions
```

Then source it in your `~/.zshrc`.
```sh
### ~/.zshrc ###
...
source ~/.config/zsh/zsh-autosuggestions/zsh-autosuggestions.zsh
source ~/.config/zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

# Aliases
Since I talk a lot about aliases in this vault, I won't go into any specific use-cases, but aliases are really handy in some certain situations. Since I have a lot of aliases, I keep them in a separate file, then source the file.

## Create Alias file
Create a new file at `~/.config/zsh/aliasrc`. This file will hold all of your aliases and short functions. Then source the file in your `~/.zshrc`.
```sh
### ~/.zshrc ###
...
source ~/.config/zsh/aliasrc
...
```

My `aliasrc` looks like this:
```sh
### ~/.config/zsh/aliasrc ###
# doas
alias s="sudo"
alias su="gum confirm 'root?' && sudo -s || echo 'never mind'"

# exa
alias ls="exa -a1 --icons --group-directories-first"
alias tree="exa -T"

alias feh="feh --no-fehbg "

alias e="$EDITOR"

# cd
alias cdtemp='cd $(mktemp -d)'
mkcd() {
	mkdir -pv "$1" && cd "$_" || exit
}
alias mkdir='mkcd'

alias wm_test="Xephyr :5 & sleep 1 ; DISPLAY=:5 "
alias neofetch="pfetch"
alias stopwatch='time cat'
alias wget='curl -O '
```

To add an alias without entering the file, I use this command:
```sh
echo "alias hello='echo hello'" >> ~/.config/zsh/aliasrc
```