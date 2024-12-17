---
layout: default
title: Installation
date: 23 04 2024
author: GG
tags: 
  - terminal
  - alacritty
---

Tumbleweed
---

```zsh
sudo zypper install alacritty
```

Useful Link:

[Alacritty - ArchWiki](https://wiki.archlinux.org/title/Alacritty)

Windows
---

```powershell
scoop install alacritty
```

Brew
---

```
brew install --cask alacritty
```

Set up font
---

## About the JetBrains Mono

– Supports Powerline

– It has italic, bold, and bold italic variants too which very useful.

– JetBrains Mono NL is the no-ligatures version of JetBrains Mono font.

## Install Font on Tumbleweed:

```zsh
sudo zypper install jetbrains-mono-fonts
```

## Check installed fonts:

```zsh
> fc-list : family style | grep -i jetbrains

JetBrains Mono,JetBrains Mono ExtraBold:style=ExtraBold Italic,Italic
JetBrains Mono,JetBrains Mono Light:style=Light Italic,Italic
JetBrains Mono,JetBrains Mono Thin:style=Thin,Regular
JetBrains Mono,JetBrains Mono ExtraLight:style=ExtraLight,Regular
JetBrains Mono,JetBrains Mono ExtraBold:style=ExtraBold,Regular
JetBrains Mono NL,JetBrains Mono NL ExtraLight:style=ExtraLight Italic,Italic
JetBrains Mono NL,JetBrains Mono NL ExtraBold:style=ExtraBold,Regular
JetBrains Mono NL,JetBrains Mono NL Light:style=Light,Regular
JetBrains Mono NL,JetBrains Mono NL ExtraLight:style=ExtraLight,Regular
JetBrains Mono:style=Bold Italic
JetBrains Mono,JetBrains Mono Light:style=Light,Regular
JetBrains Mono NL,JetBrains Mono NL Medium:style=Medium,Regular
JetBrains Mono NL,JetBrains Mono NL Thin:style=Thin,Regular
JetBrains Mono,JetBrains Mono Medium:style=Medium,Regular
JetBrains Mono,JetBrains Mono Thin:style=Thin Italic,Italic
JetBrains Mono NL,JetBrains Mono NL SemiBold:style=SemiBold,Regular
JetBrains Mono:style=Italic
JetBrains Mono,JetBrains Mono SemiBold:style=SemiBold Italic,Italic
JetBrains Mono NL:style=Regular
JetBrains Mono NL,JetBrains Mono NL Light:style=Light Italic,Italic
JetBrains Mono NL,JetBrains Mono NL SemiBold:style=SemiBold Italic,Italic
JetBrains Mono NL,JetBrains Mono NL Medium:style=Medium Italic,Italic
JetBrains Mono,JetBrains Mono SemiBold:style=SemiBold,Regular
JetBrains Mono:style=Bold
JetBrains Mono:style=Regular
JetBrains Mono NL,JetBrains Mono NL ExtraBold:style=ExtraBold Italic,Italic
JetBrains Mono,JetBrains Mono ExtraLight:style=ExtraLight Italic,Italic
JetBrains Mono NL:style=Bold Italic
JetBrains Mono NL,JetBrains Mono NL Thin:style=Thin Italic,Italic
JetBrains Mono,JetBrains Mono Medium:style=Medium Italic,Italic
JetBrains Mono NL:style=Italic
JetBrains Mono NL:style=Boldlocalhost% fc-list : family style | grep -i fira
```

## Install Font on Mac.

Download and install it from an URL like:

https://download.jetbrains.com/fonts/JetBrainsMono-2.304.zip

Open Font Book and drag the extracted font files there.

## Create an empty config file

```
mkdir -p $HOME/.config/alacritty/
touch $HOME/.config/alacritty/alacritty.toml
```

## Setup font in ``alacritty.toml``

Add the lines:

```toml
[font]
size = 13.0

[font.bold]
family = "JetBrains Mono"
style = "Bold"

[font.bold_italic]
family = "JetBrains Mono"
style = "Bold Italic"

[font.italic]
family = "JetBrains Mono"
style = "Italic"

[font.normal]
family = "JetBrains Mono"
style = "Regular"
```
  

Change color theme
---

Add the following lines to the config file

```toml
# Default colors
[colors.primary]
background = '#122637'
foreground = '#ffffff'

[colors.cursor]
text = '#122637'
cursor = '#f0cb09'

# Normal colors
[colors.normal]
black   = '#000000'
red     = '#ff0000'
green   = '#37dd21'
yellow  = '#fee409'
blue    = '#1460d2'
magenta = '#ff005d'
cyan    = '#00bbbb'
white   = '#bbbbbb'

# Bright colors
[colors.bright]
black   = '#545454'
red     = '#f40d17'
green   = '#3bcf1d'
yellow  = '#ecc809'
blue    = '#5555ff'
magenta = '#ff55ff'
cyan    = '#6ae3f9'
white   = '#ffffff'
```

Use MSYS on windows
---

Zsh must be installed in MSYS2 before this is set.

``` toml
[terminal]

[terminal.shell]
program = "C:/msys64/msys2_shell.cmd"
args = [
  "-defterm",
  "-here",
  "-use-full-path",
  "-no-start",
  "-mingw64"
  "-shell",
  "zsh"
]
```

VI mode
---

- Ctrl-Shift-Space: Turn VI mode on and off.
- HJKL: Navigate left, down, up and right.
- v: selection mode
- shift-v: line selection mode
- y: copy to clipboard

Search mode
---

- Ctrl-Shift-F: Turn on search mode.
- Enter, Shift-Enter: Search up and down.