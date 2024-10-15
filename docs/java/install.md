---
layout: default
title: Installation
date: 15 10 2024
author: GG
tags: 
  - java
---

OSX
---

This java works well with UNO

```zsh
brew install openjdk@11
```

For the system Java wrappers to find this JDK, symlink it with

```zsh
sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
```

```zsh
export CPPFLAGS="-I/opt/homebrew/opt/openjdk@11/include"
```
