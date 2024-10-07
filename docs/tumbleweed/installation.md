---
layout: default
title: Installation
date: 31 08 2024
author: GG
tags: tumbleweed, linux, amd, tuxedo
---

Installation
===

Drivers
---

Update
===

``` zsh
sudo zypper dup --allow-vendor-change --recommends
```

- *--allow-vendor-change* to allow changes to the vendor-provided packages.
- *--recommends* to install recommended packages as well.

Install dotnet
===

Tumbleweed basically works with opensuse repo

```zsh
sudo wget https://packages.microsoft.com/config/opensuse/15/prod.repo -O /etc/zypp/repos.d/microsoft-prod.repo
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper refresh
sudo zypper install dotnet-sdk-8.0
```

