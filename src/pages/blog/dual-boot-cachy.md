---
layout: ../../layouts/BasePostsLayout.astro

name: "Dual booting CachyOS with Windows"
desc: "In this guide we'll see how to install CachyOS alongside Windows."
top_desc: "Dual booting"
date: "1 November 2025"
time: "7 min"
---

# Dual booting CachyOS and Windows

<img src="/posts/dual-boot-cachy/cachy-home-screen.png" alt="Cachy Screenshot">

## Introduction

Dual booting is a process where you install two or more operating systems together without losing the ability to use either of them. Before we get into dual booting, let's briefly understand what CachyOS is.

## What is CachyOS?

CachyOS is a Linux distribution based on Arch Linux, focused on speed, stability, and customization. It is a popular Arch-based distro that is also known for gaming, as it comes pre-installed with necessary drivers out of the box. Furthermore, CachyOS also provides many of the packages from the <a href="https://aur.archlinux.org/">AUR</a> prebuilt and optimized for fast and easy usage.

CachyOS gets its name from the "Cachy" Scheduler, which is a key part of CachyOS's optimization strategy. This choice of name highlights the distribution's goal of providing a highly optimized and performant system by default.

Now that we know what CachyOS is, let's move onto the installation process!

---

# Requirements

<ol>
    <li>A Windows/Linux Computer,</li>
    <li>A USB drive, preferably 8 GB or above.</li>
    <li>At least 32 GB (recommended) space after the Windows partition</li>
</ol>

<blockquote class="warning"> ⚠️ WARNING! Everything on your USB drive will be erased! Make sure to take a backup before proceeding. </blockquote>

---

<style>

.warning {
  border-left: 4px solid #f5c542;
  background-color: rgba(255, 255, 0, 0.08);
  padding: 0.1px 15px;
  margin: 15px 0;
  border-radius: 6px;
}

</style>

# Installation Steps

### **Step 1: Preparing a Bootable USB**

<ol>
    <li>Download the latest CachyOS ISO file from the <a href="https://cachyos.org/">official CachyOS website</a>.</li>
    <li>Download Ventoy from the <a href="https://www.ventoy.net/en/download.html">official Ventoy site.</a></li>
    <li>Insert your USB drive into the computer.</li>
    <li>Open Ventoy.</li>
    <li>Make sure the correct USB device is selected.</li>
    <li>Click Install.</li>
    <li>You will now see a new device appearing by the name of "Ventoy."</li>
    <li>Simply copy your CachyOS ISO into this drive.</li>
    <li>Congratulations! We now have a bootable USB drive.</li>
</ol>

### **Step 2: Preparing BIOS Settings**

<ol>
    <li>Restart your computer and enter the BIOS by pressing a specific key.</li>
    <blockquote style="margin-bottom: 0.5em;"> This key may be different for many boards. (Usually Esc, F2, F9)</blockquote>
    <li>Look for Boot Order and move USB up to first.</li>
    <li>Now exit the BIOS and make sure the changes are saved.</li>
</ol>

### **Step 3: Initiating Installation**

<ol>
    <li>Your computer will boot into the Ventoy menu.</li>
    <li>Choose the CachyOS ISO via arrow keys, then select "Boot in normal mode."</li>
    <li>In the Grub menu, choose "CachyOS" via the arrow keys.</li>
    <li>CachyOS will start booting. The boot process may take around 5-15 minutes.</li>
    <li>Once you are booted into the live desktop environment, choose Launch installer from the welcome wizard.</li>
    <li>If asked for the bootloader, choose Grub.</li>
    <li>Configure the installation to your needs.</li>
    <li>When you reach the Partitions tab, choose manual partitioning.</li>
</ol>

### **Step 4: Creating Partitions**

CachyOS needs 2 partitions to install: bootloader/EFI and Root

<ol>
    <li>
        Click on the empty space. and then press the "Create" button.
        <ul>
            <li>Set size as 500 MiB.</li>
            <li>Set the file system to FAT32</li>
            <li>Set the mount point to <code>/boot/efi</code></li>
            <li>Select boot in the list of Flags.</li>
            <li>Click OK.</li>
        </ul>
    </li>
    <li>
        Click on the empty space left. and then press the "Create" button.
        <ul>
            <li>Set File System to ext4.</li>
            <li>Set the mount point to <code>/</code></li>
            <li>Click OK.</li>
        </ul>
    </li>
    <li>Now click next to proceed.</li>
</ol>

### **Step 5: Choosing a Desktop Environment**

A desktop environment (DE) is basically the entire UI that you'll be using. On Windows it might be fixed, but here you have the choice to choose whatever you desire. For beginners, I recommend using KDE Plasma. It has a layout similar to Windows and is very user-friendly.

Once you've chosen your desktop environment, click next.

### **Step 6: Additional Packages**

In this section you'll be seeing a choice to select any additional packages. If you have no idea what the different packages are, then just click next.

### **Step 7: Creating Users**

You will be asked to enter user details, etc. After you are done, click next.

### **Step 8: Summary**

Verify all the changes on the summary page before clicking Install.

### **Step 9: Booting into CachyOS**

After the installation is done, reboot.

Following step 2 boot back into BIOS and select CachyOS or Grub at the top of the boot priority, then save changes and exit.

After rebooting, you will see a new menu appearing. Choose CachyOS from that menu.

---

# Summary

Congratulations! 🎉 You have successfully installed CachyOS alongside Windows! Now you can use CachyOS alongside Windows whenever you want by selecting the respective OS in the menu.

---
