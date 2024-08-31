---
layout: default
title: git
date: 31 08 2024
author: GG
tags: config
---

Install Windows / Scoop
---

``` zsh
scoop install --global git
```

Configure global settings
---

``` zsh
git config --global --get core.autocrlf
```

See how to set up a compare or a merge tool like kdiff3 or meld

Configure settings for a specific repo
---

``` zsh
git config user.email "x.y@z.com"
git config user.name "X Y"
```

Reset submodules to the original state
---

``` zsh
git submodule deinit -f .
git submodule update --init

```

Find all git repos in a folder
---

``` zsh
find . -type d -name ".git" -exec dirname {} \; | sort -u
```
