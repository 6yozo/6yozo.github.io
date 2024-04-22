Tumbleweed
---
    -sudo zypper install helix

Customize settings
---

Create the file with the settings:

~/.config/helix/config.toml

:config-open will open this file for editing

Change the shell helix runs in
---

Configure the desktop shortcut for gnome

Download the desktop file into ~/.local/share/applications from:
https://github.com/helix-editor/helix/blob/master/contrib/Helix.desktop

Download the icon file into ~/.local/share/icons from:
https://github.com/helix-editor/helix/blob/master/contrib/helix.png

Modify the desktop file into something like:

[Desktop Entry]
Name=Helix in Alacritty
Comment=Edit text files
Exec=alacritty --title "Helix" --class "Helix" -e helix %F
Type=Application
Icon=helix.png
Terminal=false
Categories=Utility;TextEditor;
MimeType=text/english;text/plain;text/x-makefile;text/x-c++hdr;text/x-c++src;text/x-chdr;text/x-csrc;text/x-java;text/x-moc;text/x-pascal;text/x-tcl;text/x-tex;application/x-shellscript;text/x-c;text/x-c++;

Set up a theme for helix
---

Type :theme then type a space and start hitting tab.
The theme can be set up in config.toml like:

theme = "solarized_dark"
