---
layout: default
title: Pipe
date: 23 04 2024
author: GG
tags: 
  - helix
  - editor
  - pipe
---

Helix can pipe selected lines and pass them as input to any command,
and then replace the selected lines with the output of the command.

format the selected text to 80 columns:

```
| fmt -w 80
```
