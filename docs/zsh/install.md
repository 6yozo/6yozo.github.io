---
layout: default
title: ZSH
date: 23 04 2024
author: GG
tags: zsh
---

Installation
---

Determine the location of the shell

```
which zsh
```
    
then change the shell

```
chsh -s /usr/bin/zsh
```

Log out of your computer and log back in!

After starting zsh for the first time some settings can be adjusted.

Set history file size limits to 1 000 000.

The .zshrc file
---

```
# Lines configured by zsh-newuser-install
HISTFILE=~/.histfile
HISTSIZE=1000000
SAVEHIST=1000000
unsetopt beep
bindkey -v
# End of lines configured by zsh-newuser-install
# The following lines were added by compinstall
zstyle :compinstall filename '/home/gg/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall

## Colorize the ls output ##
alias ls='ls --color=auto'
```

Make Helix the default editor
---

# Make Helix the default editor for command-line tasks
```
export EDITOR=helix
```

Set up liquidprompt
---

```
git clone --branch stable https://github.com/nojhan/liquidprompt.git ~/liquidprompt
```

Then add to ``.zshrc``:

```
# Setup Liquidprompt with Powerline theme
setup_liquidprompt() {
    LP_ENABLE_TIME=1
    LP_TIME_FORMAT="%Y-%m-%dT%H:%M:%S"
    LP_PS1_PREFIX='{*]>'
    LP_PATH="$HOME/liquidprompt"
    
    if [ ! -f "${LP_PATH}/liquidprompt" ]; then
        echo "Error: Liquidprompt script not found."
        return 1
    fi
    
    if [ ! -f "${LP_PATH}/themes/powerline/powerline.theme" ]; then
        echo "Error: Powerline theme file not found."
        return 1
    fi

    . "${LP_PATH}/liquidprompt"
    . "${LP_PATH}/themes/powerline/powerline.theme"    

    if ! type lp_theme &>/dev/null; then
        echo "Error: lp_theme function is not available."
        return 1
    fi
    
    lp_theme powerline_full
}
LP_DISABLED_VCS_PATHS=(
    "/c/QMK_MSYS/home/gaspa/qmk_firmware_sequitap/users/sequitap" 
    "/c/Workspace/nFlow2"
)
setup_liquidprompt
```

Vi navgation
---

To get into command mode, press [ESC]
To return to insert mode, simply type i,

- $ go the end of the line or
- 0 go to the beginning of the line.
- b to go back one word
- 2b to go back two words
- dw to delete a word
- dd to delete the entire line
- d$ to delete from the current cursor position to the end of the line
- d0 to delete from the current cursor position to the beginning of the line
- w to go forward one word, and so forth
