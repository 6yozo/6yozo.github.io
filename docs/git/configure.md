---
layout: default
title: git
date: 01 05 2024
author: GG
tags: config
---

Install Windows / Scoop
---

``` powershell
scoop install --global git
```

Configure global settings
---

``` powershell
git config --global --get core.autocrlf
```

See how to set up a compare or a merge tool like kdiff3 or meld

Configure settings for a specific repo
---

``` powershell
git config user.email "x.y@z.com"
git config user.name "X Y"
```

Reset submodules to the original state
---

git submodule deinit -f .
git submodule update --init
