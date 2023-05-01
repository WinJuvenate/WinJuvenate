# WinJuvenate

---
Note: This repository is still heavily under development. 
---

WinJuvenate is a set of PowerShell scripts that help you to create a minimal Window installation.

Currently supported Windows version:

* Windows 11 Pro AMD64, Build (WIP), Languages: (WIP) 

With these scripts you can:
* download the latest Windows 11 (en_US) ISO from Microsoft.
* alternatively provide your own ISO.
* build a trimmed-down Windows 11 installer ISO.

## Origins

This project is based on existing findings and scripts by other community members. I am more than happy to open up for additional maintainer or re-join it with any other fork if the ideas and goals align.

* Original idea based on [tiny11 (by ntdevlabs)](https://github.com/ntdevlabs/tiny11builder)
* PowerShell rewrite by [ianis58's fork](https://github.com/ianis58/tiny11builder)


## Features

The goal is to remove as many as possible additional Windows features while keeping the core system functions intact. No extra software is installed (might make exceptions to improve minimal Windows experience).

Removed components:

* See [this JSON file](/config.json)

Included autounattend.xml file:

* bypasses the need to connect to/create a Microsoft account during OOBE (Out Of the Box Experience)
* automatically accepts the EULA (End User Licence Agreement)
* skips the product key step (uses Windows 10 or 11 key from EFI/UEFI if it exists, otherwise you'll be able to set it after installation

Minimal tweaks: (To be re-evaluated)

* dark theme enabled by default
* some file explorer config turned on: show hidden files, show known file extensions, ...
* taskbar aligned to the left

## Running it

1. Download this repository as zip and unzip it where you want.
2. Open a Powershell as administrator, go to the extraction path, and run the following commands:
```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\tiny11creator.ps1
```
3. Sit back and relax :) (it runs for 25 minutes approximately on my old-but-decent laptop). You might see some errors with RemoveWindowsPackage, but it's not an issue (has to do with the order and dependencies of packages to remove).
4. The created Windows 11 installer iso is available in c:\tiny11.iso

### Optional:

5. After setup and once connected to the internet, I recommend to install the package manager from Microsoft called winget. Run this command in PowerShell:
```
Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe
```
Then you can run one of these to get your favorite browser:
```
winget install Mozilla.Firefox
winget install Microsoft.Edge
winget install Opera.Opera
winget install Google.Chrome
```
