# PXE Server Installation

![Version](https://img.shields.io/badge/version-2.0-blue) ![Platform](https://img.shields.io/badge/platform-Ubuntu%2024.04-orange)

**Version:** 2.0  
**Last Update:** 2026/04/14  
**Author:** Jasper Lee  

This project builds a PXE server based on **Ubuntu 24.04.3 Desktop**, integrating `Apache2`, `iPXE`, `TFTP`, and `HTTP` services, with support for both IPv4 and IPv6 environments.


## Table of Contents
- [PXE Server Installation](#pxe-server-installation)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Notice](#notice)

---
## Features
* IPv4 / IPv6 PXE boot support
* Automated DHCP / TFTP / Apache setup
* iPXE custom menu integration
* ISO auto-mount and dynamic PXE boot menu generation

## Prerequisites

- **OS**: Ubuntu 24.04.3 Desktop (recommended)
- **Network**: Internet connection required during installation
- **Privileges**: Root or sudo access
- **ISO**: At least one Ubuntu ISO file prepared

## Installation

> If you cloned this repository from GitHub, you can **skip Step 1–2**.

1. **Extract the package** *(skip if using GitHub clone)*
   ```bash
   sudo tar xzvf pxe-installer-v2.0.tar.gz
   ```

2. **Enter the project directory** *(skip if using GitHub clone)*
   ```bash
   cd pxe-installer-v2.0
   ```

3. **Configure environment variables**
   ```bash
   cp config.env.example config.env
   nano config.env
   ```
   Edit `config.env` based on your network environment.

4. **Prepare installation ISO**
   * Place at least one Ubuntu ISO file in your defined `ISO_PATH`
   * Ensure the path is correctly set in `config.env`

5. **(Optional) Set up WinPE environment**
   * Configure a Samba server
   * Modify `/pxe/http/WinPE/startup.bat` (if the file exists)

6. **Run the installation script**
   ```bash
   sudo ./pxe-v2.0.sh
   ```

7. **Check available options**
   ```bash
   sudo ./pxe-v2.0.sh -h
   ```

## Notice 
1. **Internet connection is required**
   Ensure the PXE host has Internet access during installation (for package installation and dependency setup).

2. **Optional components and NDA restrictions**

   Some components are **not included in this repository** due to licensing and NDA restrictions.

   The following components will **NOT** be provided publicly:

   * EFI Shell
   * WinPE
   * Ghost

   This repository focuses on the **deployment framework and automation logic only**. The full installation package (`pxe-installer-v2.0.tar.gz`) is not included in this public repository. It contains:

   * `pxe-v2.0.sh`
   * `README.md`
   * `config.env.example`
   * `script/pxe-mount-iso.sh`
   * `script/pxe-umount-iso.sh`

   For internal/company use, a complete installation package (including these components) may be distributed separately.

   To enable full functionality, you may:

   * Refer to the installation logs for manual file placement
   * Copy required files into the PXE environment manually
   * Follow official documentation (e.g., Microsoft WinPE) for setup

   Some PXE menu options will not function if these components are not installed.

3. **Line ending issue (CRLF)**
   If you encounter the error:

   ```bash
   sudo: unable to execute ./pxe-v2.0.sh: No such file or directory
   ```

   Convert the script format:

   ```bash
   sudo apt update
   sudo apt install dos2unix -y
   dos2unix ./pxe-v2.0.sh
   ```
