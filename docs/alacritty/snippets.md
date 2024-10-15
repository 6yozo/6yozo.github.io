---
layout: default
title: Snippets
date: 23 04 2024
author: GG
tags: 
  - terminal
  - alacritty
---

Which shell am I running
---

To find the shell you have on the default environment you can check the value of the SHELL environment variable:

```
echo $SHELL
```

To find the current shell instance, look for the process (shell) having the PID of the current shell instance.

To find the PID of the current instance of shell:

```
echo "$$"
```

Now to find the process having the PID:

```
ps -p <PID>
```

Putting it together:

```
ps -p "$$"
```
