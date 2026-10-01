---
title: "Dual booting CachyOS with Windows"
date: "2025-11-01"
draft: false
description: "In this guide we'll see how to install CachyOS alongside Windows."
showToc: true
tags: ["dual boot", "cachyos", "linux", "grub"]
---

![Cachy Screenshot](/dual-boot-cachy/cachy-home-screen.webp)

## Introduction

Dual booting is a process where you install two or more operating systems together without losing the ability to use either of them. Before we get into dual booting, let's briefly understand what CachyOS is.

## What is CachyOS?

CachyOS is a Linux distribution based on Arch Linux, focused on speed, stability, and customization. It is a popular Arch-based distro that is also known for gaming, as it comes pre-installed with necessary drivers out of the box. Furthermore, CachyOS also provides many of the packages from the [AUR](https://aur.archlinux.org/) prebuilt and optimized for fast and easy usage.

CachyOS gets its name from the "Cachy" Scheduler, which is a key part of CachyOS's optimization strategy. This choice of name highlights the distribution's goal of providing a highly optimized and performant system by default.

Now that we know what CachyOS is, let's move onto the installation process!

---

## Requirements

1. A Windows/Linux Computer
2. A USB drive, preferably 8 GB or above
3. At least 32 GB (recommended) space after the Windows partition

> ⚠️ **WARNING:** Everything on your USB drive will be erased! Make sure to take a backup before proceeding.

---

# Installation Steps

### Step 1: Preparing a Bootable USB

1. Download the latest CachyOS ISO file from the [official CachyOS website](https://cachyos.org/).  
2. Download Ventoy from the [official Ventoy site](https://www.ventoy.net/en/download.html).  
3. Insert your USB drive into the computer.  
4. Open Ventoy.  
5. Make sure the correct USB device is selected.  
6. Click Install.  
7. You will now see a new device appearing by the name of "Ventoy."  
8. Simply copy your CachyOS ISO into this drive.  
9. Congratulations! You now have a bootable USB drive.

### Step 2: Preparing BIOS Settings

1. Restart your computer and enter the BIOS by pressing a specific key.  
   > This key may be different for many boards. (Usually Esc, F2, F9)  
2. Look for Boot Order and move USB up to first.  
3. Exit the BIOS and make sure the changes are saved.

### Step 3: Initiating Installation

1. Your computer will boot into the Ventoy menu.  
2. Choose the CachyOS ISO via arrow keys, then select "Boot in normal mode."  
3. In the Grub menu, choose "CachyOS" via the arrow keys.  
4. CachyOS will start booting. The boot process may take around 5-15 minutes.  
5. Once booted into the live desktop environment, choose Launch installer from the welcome wizard.  
6. If asked for the bootloader, choose Grub.  
7. Configure the installation to your needs.  
8. When you reach the Partitions tab, choose manual partitioning.

### Step 4: Creating Partitions

CachyOS needs 2 partitions to install: bootloader/EFI and Root

1. Click on the empty space, then press "Create":  
   - Set size as 500 MiB  
   - File system: FAT32  
   - Mount point: `/boot/efi`  
   - Flag: boot  
   - Click OK  

2. Click on the remaining empty space, then press "Create":  
   - File system: ext4  
   - Mount point: `/`  
   - Click OK  

3. Click Next to proceed.

### Step 5: Choosing a Desktop Environment

A desktop environment (DE) is the UI you’ll be using. For beginners, KDE Plasma is recommended as it is user-friendly and has a layout similar to Windows.  

Once you've chosen your DE, click Next.

### Step 6: Additional Packages

Select any additional packages if desired. If unsure, just click Next.

### Step 7: Creating Users

Enter user details as prompted. Then click Next.

### Step 8: Summary

Verify all the changes on the summary page before clicking Install.

### Step 9: Booting into CachyOS

After installation, reboot.  

Return to BIOS and select CachyOS or Grub at the top of the boot priority, then save changes and exit.  

After rebooting, a new menu will appear — choose CachyOS.

---

# Summary

🎉 Congratulations! You have successfully installed CachyOS alongside Windows. You can now select either OS from the boot menu whenever you want.

---