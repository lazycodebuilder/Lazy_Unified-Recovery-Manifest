# Lazy Unified Recovery Manifest

## Overview

Lazy Unified Recovery Manifest is a repository that simplifies building custom recoveries from source. It provides a structured and unified manifest for syncing different recovery sources, making the build process easier for developers.

## Features

- Unified manifest supporting multiple recovery projects
- Supports multiple recovery sources
- Simplified source syncing process
- Easy-to-use XML format for repository management

## Supported Recovery Projects

- **Minimal TWRP Manifest** - [`twrp-12.1`](https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git)
- **SHRP Manifest** - [`shrp-12.1`](https://github.com/SHRP-Reborn/manifest.git)
- **PitchBlack Recovery Manifest** - [`android-12.1`](https://github.com/PitchBlackRecoveryProject/manifest_pb.git)

## Prerequisites

- A Linux-based environment ([Ubuntu/Debian recommended](https://ubuntu.com/download)) or **Windows with WSL** ([Setup Guide](https://docs.microsoft.com/en-us/windows/wsl/install))
- Repo tool installed ([Installation Guide](https://source.android.com/docs/setup/develop/repo))
- At least **100GB of free disk space** (varies depending on the recovery project)
- Git installed ([Download Git](https://git-scm.com/downloads))

## Setup Guide

### 1. Configure Git

```bash
git config --global user.email "your-email@example.com"
git config --global user.name "Your Name"
```

### 2. Navigate to the synced directory

```bash
cd <source-dir>
```

### 3. Initialize the Source Code

```bash
repo init --depth=1 -u https://github.com/lazycodebuilder/Lazy_Unified-Recovery-Manifest.git -b android-12.1
```

### 4. Choose Recovery Project

To switch from TWRP to SHRP or PBRP, run:

```bash
sed -i "s/twrp/shrp/g" .repo/manifests/select-project.xml  # Replace 'shrp' with 'pbrp' if needed
```

### 5. Sync the Source Code

```bash
repo sync -c -j$(nproc --all)
```

## Building the Recovery

### 1. Set Up Build Environment

```bash
export ALLOW_MISSING_DEPENDENCIES=true
. build/envsetup.sh
lunch twrp_<device>-eng
```

### 2. Build Commands

#### **TWRP/SHRP**

- **Recovery partition:**
  ```bash
  mka recoveryimage | tee out/<codename>-rec.log
  ```
- **Boot image ramdisk:**
  ```bash
  mka bootimage | tee out/<codename>-rec.log
  ```
- **Vendor_boot image ramdisk:**
  ```bash
  mka vendorbootimage | tee out/<codename>-rec.log
  ```

#### **PitchBlack Recovery (PBRP)**

- **Recovery partition:**
  ```bash
  mka pbrp # Builds a flashable ZIP
  ```
- **Boot image ramdisk:**
  ```bash
  mka pbrp # Builds a flashable ZIP
  ```
- **Vendor_boot image ramdisk:**
  ```bash
  mka vendorbootimage
  ```

## Contribution

Contributions are welcome! Fork the repository, make your changes, and submit a pull request.

## Contact

For issues and discussions, open an issue in the repository or join GitHub discussions.

