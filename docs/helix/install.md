---
layout: default
title: Installation
date: 23 04 2024
author: GG
tags: 
  - helix
  - editor
---

Tumbleweed
---

```zsh
sudo zypper install helix
```

Windows
---

```powershell
scoop install helix
```

Mac
–––

```
brew install helix
```


Customize settings
---

Create the file with the settings:

``:config-open`` will open this file for editing

Configure the desktop shortcut for mac
---

## Mac

Open Automator, choose Application, add a Run Shell Script action and put in:

```
/Applications/Alacritty.app/Contents/MacOS/alacritty --title "Helix" --class "Helix" -e /opt/homebrew/bin/hx
```

Save it as an Application, give it the name "Helix". Move it into the Applications folder.

Download the icon file into ``~/.local/share/icons`` from:

```
https://github.com/helix-editor/helix/blob/master/contrib/helix.png
```

Open Get Info on the Automator Application and drag and drop the icon on the old icon to replace it.
	
## Tumbleweed

Download the desktop file into ``~/.local/share/applications`` from:
[Helix](https://github.com/helix-editor/helix/blob/master/contrib/Helix.desktop)

Download the icon file into ``~/.local/share/icons`` from:

```
https://github.com/helix-editor/helix/blob/master/contrib/helix.png
```

Modify the desktop file into something like:

```ini
[Desktop Entry]
Name=Helix in Alacritty
Comment=Edit text files
Exec=alacritty --title "Helix" --class "Helix" -e helix %F
Type=Application
Icon=helix.png
Terminal=false
Categories=Utility;TextEditor;
MimeType=text/english;text/plain;text/x-makefile;text/x-c++hdr;text/x-c++src;text/x-chdr;text/x-csrc;text/x-java;text/x-moc;text/x-pascal;text/x-tcl;text/x-tex;application/x-shellscript;text/x-c;text/x-c++;
```

Set up a theme for helix
---

Type ``:theme`` then type a space and start hitting tab.
The theme can be set up in ``config.toml`` like:

```
theme = "solarized_dark"
```
