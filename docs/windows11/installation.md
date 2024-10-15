---
layout: default
title: Installation
date: 30 06 2023
author: GG
tags: 
  - windows 11
  - amd
  - tuxedo
  - scoop
---

Installation
===

Drivers
---

When installing Windows 11 on a notebook, download the official
drivers for your notebook. I use a Tuxedo Pulse v1, so in my case the
drivers are here:

[Tuxedo Pulse v1 Drivers](https://mytuxedo.de/index.php/s/ZeB8FTf8CrpEtJr?path=%2FPulse_Series)

<!--
Set up dark moden
===

- Personalization / Themes
- Windows (dark)

-->

Wrong installation of AMD drivers
---

The AMD driver must be reinstalled when the following message appears:

> C:\Windows\SYSTEM32\amdihk32.dll is either not designed to run on
> Windows or it contains an error. Try installing the program again
> using the original installation media or contact your system
> administrator or the software vender for support.

Or in Hungarian

> A(z) C:\Windows\SYSTEM32\amdihk32.dll nem Windows rendszerhez lett
> tervezve, vagy hibat tartamaz. Probalja ujratelepiteni a programot
> az eredeti telepitolemezrol, vagy forduljon a rendszergazdahoz,
> illetve a program forgalmazojahoz. Hibaallapot: 0x000012f.

The name of the dll sometimes is different.

Download the AMD driver:

[AMD Software: Adrenalin Edition](https://www.amd.com/en/support/apu/amd-ryzen-processors/amd-ryzen-7-mobile-processors-radeon-graphics/amd-ryzen-7-4800h)

Uninstall the driver by running:

> Driver-AMD_VGA_OEM_ORIGINAL\Bin64\AMDCleanupUtility.exe

Then reinstall it.


Install and setup Scoop to manage installed applications
---

Instal Scoop from ``scoop.sh`` using the Advanced Installation Method.
This will let us configure directories so virus checkers can be set up
to ignore these folders.

Download the installer script:

Open PowerShell and run the following command to download the Scoop
installation script:

``` powershell
irm get.scoop.sh -outfile 'install.ps1'
```

To understand all the options you can configure during installation, execute:

``` powershell
.\install.ps1 -?
```

Install Scoop to a custom directory and set a custom directory for
globally installed programs:

``` powershell
.\install.ps1 -ScoopDir 'C:\Workspace\Programs\Scoop' -ScoopGlobalDir 'C:\Workspace\Programs\GlobalScoopApps'
```

Install JetBrains Mono font
---

This is a coding friendly font.

``` powershell
scoop bucket add nerd-fonts
scoop install --global JetBrains-Mono
```

The recommended Font settings are:

Size: 13
Line spacing: 1.2

Install 7zip
---

``` powershell
scoop install --global 7zip
```
