---
tags:
- linux
---

## **Linux File System

###  [Filesystem Hierarchy Standard (FHS)](https://dev.to/prodevopsguytech/understanding-the-linux-filesystem-an-in-depth-guide-for-devops-engineers-ona?ref=dailydev#2-filesystem-hierarchy-standard-fhs)

The Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux systems. Adherence to FHS ensures that software behaves predictably across different Linux distributions.

The root directory (`/`) serves as the starting point of the filesystem. Key subdirectories include:

- **`/bin`**: Essential command binaries, like `ls`, `cp`, and `mv`.
- **`/boot`**: Bootloader files, including the kernel.
- **`/dev`**: Device files representing hardware components.
- **`/etc`**: Configuration files for the system.
- **`/home`**: User home directories.
- **`/lib`**: Essential shared libraries.
- **`/mnt`**: Temporary mount points for filesystems.
- **`/opt`**: Optional software packages.
- **`/proc`**: Virtual filesystem providing process and kernel information.
- **`/root`**: Home directory for the root user.
- **`/sbin`**: System binaries, typically for administrative tasks.
- **`/tmp`**: Temporary files.
- **`/usr`**: Secondary hierarchy for user programs and data.
- **`/var`**: Variable data files like logs, databases, and email.
- ### [Important Directories and Their Purposes](https://dev.to/prodevopsguytech/understanding-the-linux-filesystem-an-in-depth-guide-for-devops-engineers-ona?ref=dailydev#5-important-directories-and-their-purposes)

Each directory in the Linux filesystem has a specific role. Here’s a deeper look into some of the most critical directories:

- **`/` (Root Directory)**: The starting point of the filesystem. All other directories and files branch off from here.
- **`/bin`**: Contains essential command binaries needed for the system to function in single-user mode. These are available to all users.
- **`/sbin`**: Similar to `/bin`, but contains system binaries that are typically used by the root user for administrative tasks.
- **`/lib`**: Contains shared libraries required by the binaries in `/bin` and `/sbin`.
- **`/usr`**: A secondary hierarchy that contains user programs, libraries, documentation, and more. It’s split into subdirectories like `/usr/bin`, `/usr/sbin`, and `/usr/lib`.
- **`/var`**: Stores variable data like logs, databases, and spools. This directory often grows in size over time.
- **`/etc`**: The nerve center for system configuration files. Nearly every service or application has a configuration file located here.
- **`/home`**: Contains personal directories for each user. This is where users store their personal files and directories.
- **`/proc`**: A virtual filesystem that provides an interface to kernel data structures. It’s used to access process information, kernel parameters, and more.
- **`/dev`**: Contains device files that represent hardware components. These files act as interfaces to the corresponding hardware.

[[Linux]]