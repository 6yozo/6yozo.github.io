---
layout: default
title: ZSH
date: 23 04 2024
author: GG
tags: zsh
---

Installation
===

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

MSYS2 does not have chsh but zsh can be made the default by changing 
Alacritty settings.

The .zshrc file
===

Settings for both interactive and non-interactive shells
---

### History

```zsh
# Lines configured by zsh-newuser-install
HISTFILE=~/.histfile
HISTSIZE=1000000
SAVEHIST=1000000
unsetopt beep
bindkey -v
# End of lines configured by zsh-newuser-install
```

### Compinstall

```zsh
# The following lines were added by compinstall
zstyle :compinstall filename '/home/gg/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall
```

### Make Helix the default editor

Make Helix the default editor for command-line tasks

```zsh
export EDITOR=helix
alias hx='helix'
```

Settings for interactive mode
===

Ignore the rest for non-interactive shells
---

```zsh
# Do not run the rest of the script if the shell is not interactive.
# This can help avoid unintended behaviors in scripts, cron jobs, or other 
# automated tasks that might source this configuration file.
case $- in
    *i*) ;;
    *) return;;
esac
```

Set up liquidprompt
---

Remove any `.liquidpromptrc` in the `.configuration` folder or in any other 
folder where it gets loaded automatically. This ensures that the settings in
`.zshrc` can take effect.

```
git clone --branch stable https://github.com/nojhan/liquidprompt.git ~/liquidprompt
```

Then add to ``.zshrc``:

```zsh
# Setup Liquidprompt with Powerline theme
export LP_PATH="$HOME/liquidprompt"
export LP_ENABLE_TIME=1
export LP_TIME_FORMAT="%Y-%m-%dT%H:%M:%S"
export LP_PS1_PREFIX='{*]>'
export LP_ALWAYS_DISPLAY_VALUES=1
export LP_DISPLAY_VALUES_AS_PERCENTS=1
LP_DISABLED_VCS_PATHS=(
    "/c/QMK_MSYS/home/gaspa/qmk_firmware_sequitap/users/sequitap"
    "/c/Workspace/nFlow2"
)
export LP_DISABLED_VCS_PATHS
setup_liquidprompt() {    
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
setup_liquidprompt
```

Colorize things
---

```zsh
# Enble colors in Zsh
autoload -U colors && colors

# ls command with colors
alias ls='ls --color=auto'

# grep with colors
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Enable colored output for diff
alias diff='diff --color=auto'

# Git colored outputalias
git='git --no-pager'

# Add color to less if possible
export LESS='-R'

# Man pages
export LESS_TERMCAP_mb=$'\e[1;31m'   # begin blinking
export LESS_TERMCAP_md=$'\e[1;31m'   # begin bold
export LESS_TERMCAP_me=$'\e[0m'      # end mode
export LESS_TERMCAP_se=$'\e[0m'      # end standout-mode
export LESS_TERMCAP_so=$'\e[1;44;33m' # begin standout-mode - info box
export LESS_TERMCAP_ue=$'\e[0m'      # end underline
export LESS_TERMCAP_us=$'\e[1;32m'   # begin underline
```

Vi navgation
===

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

TODO:
===
Create a script which can update things installed from source like liquibase
