---
{"dg-publish":true,"permalink":"/thm-notes/linux-n/linux-structure/","title":"Linux Structure","tags":["linux"]}
---

# NOTES

---

- **Components of Linux**
    
    Boot Loader
    
    OS kernel
    
    Daemons
    
    OS Shell
    
    Graphics server
    
    windows manager
    
    Utilities
    
- **Linux Architecture**
    
    Hardware
    
    kernel
    
    shell
    
    System utilities
    
- **Linux System Hierarchy**
    
    ![[Untitled.png\|Untitled.png]]
    
    Linux File System Hierarchy - > [Click Here for the source](https://enterprise.hackthebox.com/academy-lab/692/3035/modules/18/94)
    
    **/bin** - which has all the system binary files required for system maintenance, recovery, and basic system functionality **COMMAND BINARIES** . Ex : ls , cat , cp , mv
    
    **/boot** - The files required to boot the system like bootloader exec files etc.,
    
    **/dev -** Which has all the necessary files that will help the system to manage / to control the all attached hardware things
    
    **/etc -** Which has local system configuration files
    
    **/lib** - Shared library files required for the system boot
    
    **/media -** External Removable Media like USB or any media device files
    
    **/mnt -** Temporary mount point for regular filesystems.
    
    **/opt -** Optional files such as third party applications , services file are there
    
    **/home -** It has a subdirectory for all users on the system for storage files
    
    **/var -** This directory contains variable data files such as log files, email in-boxes, web application related files, cron files, and more.
    
    **/usr -** Contains executables, libraries, man files, etc.
    
    **/tmp -** Contains temporary files that will be saved by many applications ad services and they will be deleted after the boot
    
    **/sys** - The `/sys` directory in Linux is a virtual file system that  
    exposes kernel parameters and device attributes, allowing users to  
    interact with and configure the kernel and hardware. It provides  
    information and settings for system administrators and developers,  
    making it a valuable resource for managing the Linux system.  
    
    **/proc -** The `/proc` directory in Linux is a virtual file system that  
    provides information about running processes, system status, and  
    configuration. It offers a way to access details about the system's  
    memory, CPU, devices, and currently running programs through special  
    files and directories.