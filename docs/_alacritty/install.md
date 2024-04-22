Tumbleweed
---

sudo zypper install alacritty

Useful Link:

https://wiki.archlinux.org/title/Alacritty

Set up font
---

Install Font:

sudo zypper install jetbrains-mono-fonts

Check installed fonts:

gg  ~  fc-list : family style | grep -i jetbrains

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

Setup font in $HOME/.config/alacritty/alacritty.toml

[font]
size = 13.0

[font.bold]
family = "JetBrains Mono
style = "Bold"

[font.bold_italic]
family = "JetBrains Mono
style = "Bold Italic"

[font.italic]
family = "JetBrains Mono
style = "Italic"

[font.normal]
family = "JetBrains Mono
style = "Regular"

Change color theme
---

create a config file in $HOME/.config/alacritty/alacritty.toml with content:

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

