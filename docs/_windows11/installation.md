---
layout: default
title: Installation
date: 30 06 2023
author: GG
tags: windows 11, amd, tuxedo
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
