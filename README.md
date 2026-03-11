# APT and Package Management Exercise Report

##  Author Information
- **Name:** MinhLe
- **Class ID:** BEIRP25A6
- **System Name:** Robo (Ubuntu/Debian Environment)

---

##  Part 1: Understanding APT & System Updates

### 1. Check APT Version
- **Command:** `apt --version`
- **Output:** `apt 2.4.8 (amd64)` (Verified on local system)



### 2. Update the Package List
- **Command:** `sudo apt update`
- **Why is this step important?** This command synchronizes the local package index with the remote repositories. It ensures that the system is aware of the newest versions, security patches, and dependencies available before any installation or upgrade takes place.

### 3. Upgrade Installed Packages
- **Command:** `sudo apt upgrade -y`
- **Difference between `update` and `upgrade`:**
    - `update`: Refreshes the **list** (metadata) of available software.
    - `upgrade`: Downloads and **installs** the actual newer versions of the software currently on the system.

### 4. View Pending Updates
- **Command:** `apt list --upgradable`
- <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/39c36a4c-2b05-4553-8861-cc6ff358194d" />
---

## Part 2: Installing & Managing Packages

### 1. Search for a Package
- **Command:** `apt search image editor`
- **Selected Package:** `gimp` (GNU Image Manipulation Program)

### 2. View Package Details
- **Command:** `apt show gimp`
- **Dependencies:** `gimp` requires several libraries to function, such as `libgimp2.0`, `libc6`, and `libgegl-0.4-0`.

### 3. Install the Package
- **Command:** `sudo apt install gimp -y`

### 4. Check Installed Version
- **Command:** `apt list --installed | grep gimp`
- **Output:** `gimp/jammy,now 2.10.30-1build1 amd64 [installed]` (Example)

---
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a2d3f390-383b-4505-a10e-2df3e8ee1942" />

##  Part 3: Removing & Cleaning Packages

### 1. Uninstall the Package
- **Command:** `sudo apt remove gimp -y`
- **Status:** The application binaries are removed, but the configuration files remain on the system.

### 2. Remove Configuration Files (Purge)
- **Command:** `sudo apt purge gimp -y`
- **Difference between `remove` and `purge`:**
    - `remove`: Deletes the program files but keeps the settings.
    - `purge`: Deletes the program **and** all associated configuration files for a clean slate.

### 3. Clear Unnecessary Dependencies
- **Command:** `sudo apt autoremove -y`
- **Importance:** This removes "orphan" packages that were originally installed to support other software but are no longer needed, saving disk space and keeping the system lean.

### 4. Clean up Downloaded Package Files
- **Command:** `sudo apt clean`
- **Function:** This clears the local cache of downloaded `.deb` files stored in `/var/cache/apt/archives`.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/758e3279-186b-423a-9c92-25e7bc238c0d" />

---

##  Part 4: Managing Repositories & Troubleshooting

### 1. List All APT Repositories
- **Command:** `cat /etc/apt/sources.list`
- **Observations:** This file contains the URLs of official Ubuntu mirrors (Main, Restricted, Universe, and Multiverse) where the system fetches software.

### 2. Add Universe Repository
- **Command:** `sudo add-apt-repository universe` followed by `sudo apt update`
- **Universe Repository:** This repository contains free and open-source software maintained by the community, rather than Canonical (the company behind Ubuntu).

### 3. Simulate Installation Failure
- **Command:** `sudo apt install fakepackage`
- **Error Message:** `E: Unable to locate package fakepackage`
- **Troubleshooting Steps:** 1. Check the spelling of the package name.
    2. Run `sudo apt update` to refresh the index.
    3. Verify if the package requires a specific PPA or repository that has not been enabled yet.

---

##  Bonus Challenge
I tested the package locking feature to prevent unintended updates.
- **Hold Command:** `sudo apt-mark hold gimp`
- **Unhold Command:** `sudo apt-mark unhold gimp`
- **Reasoning:** Holding a package is essential when you need a specific version to remain unchanged, such as when a newer version is known to have bugs or is incompatible with existing robotics projects/libraries.
<img width="882" height="846" alt="image" src="https://github.com/user-attachments/assets/707aa69d-551d-4056-9831-63b073c013ad" />

---
