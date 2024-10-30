---
layout: default
title: KDiff
date: 01 05 2024
author: GG
tags: 
  - kdiff
  - comparision
  - merge
---

Windows / Scoop
---

``` powershell
scoop bucket add extras
```

``` powershell
scoop install --global kdiff3
```

Mac / Brew
---

```zsh
brew install kdiff3
```

Configure
---

## Font

Change ``File View Font`` to JetBrans mono 13.

## Editor

Turn on:
- Tab inserts space

Set Tab Size to 4 spaces

Turn off:
- auto indentation.

Set Line end style to Autodetect

## Regional Settings

Turn on ``Use the same encoding for everything``.

Set File Encoding for A to UTF-8

Git integration
---

``` powershell
git config --global diff.tool kdiff3
git config --global merge.tool kdiff3

# Configure the path to KDiff3 executable so it will not use scoop shims
git config --global mergetool.kdiff3.path "/c/Workspace/Programs/GlobalScoopApps/apps/kdiff3/1.11.0/bin/kdiff3.exe"

# Automatically launch KDiff3 without a prompt
git config --global mergetool.prompt false

# Set KDiff3 command line options for diff
git config --global difftool.kdiff3.cmd 'kdiff3 "$LOCAL" "$REMOTE"'

# Set KDiff3 command line options for merge
git config --global mergetool.kdiff3.cmd 'kdiff3 "$BASE" "$LOCAL" "$REMOTE" -o "$MERGED"'
```

An example config snippet
---

``` powershell
[diff]
	tool = kdiff3
[difftool]
	prompt = true
[difftool "kdiff3"]
	cmd = kdiff3 "$LOCAL" "$REMOTE"
	path = kdiff3.exe
[merge]
	tool = kdiff3
[mergetool]
	prompt = true
[mergetool "kdiff3"]
	cmd = kdiff3 "$BASE" "$LOCAL" "$REMOTE" -o "$MERGED"
	path = /c/Workspace/Programs/GlobalScoopApps/apps/kdiff3/1.11.0/bin/kdiff3.exe
```
