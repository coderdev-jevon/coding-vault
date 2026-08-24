
# Chapter 2: Linux Philosophy and Concepts
Date: 2026-08-06

Goal for this chapter:
1. Define common Linux terms
2. Discuss components of Linux distribution

## ** Linux History
Linux is open source computer OS, initially developed for Intel x86-based personal computers.

Linus Torvalds developed Linux kernel. Then Linux kernel was re-licensed under General Public License by Free Software Foundation (FSF), enabling it to build a worldwide community of developers, at last, developers created complete systems called Linux Distributions.

#### ** History of Linux

![[linux-history.png|279]]

#### ** Linux Use Cases
![[linux-usecase.png|300]]


## * Linux Philosophy
Like UNIX, Linux organizes data using a hierarchical filesystem, with `/` as the root directory for other files and directories. Linux almost treat everything like file-like objects, even network connections are managed using the same utilities as regular files.

Linux is a multitasking and multiuser OS, it includes networking capabilities and relies on background service processes called daemons (concept inherited from UNIX) to handle system and network tasks.

## * Linux Community
[Website](https://www.linux.com/)

## * Linux Terminology and Examples
#### ** 1. Kernel
Glue between hardware and applications, core of OS , example, Linux Kernel
[Linux Kernel](https://kernel.org/)
#### **  2. Distribution / Distros
Collection of programs, software, combined with Kernel to make up Linux-based OS, OS is the main manager software of computer/phone.
#### ** 3. Boot Loader
Program that boots or turns on the operating system, example, GRUB and ISOLINUX
#### ** 4. Service
Program that runs as a background process, example, `httpd, nfsd, ntpd, ftpd, and named`
#### ** 5. File system
Methods for storing and organizing files, example, `ext3, ext4, FAT< XFS, NTFS, and Btrfs`
#### ** 6. X Window System
Provide standard toolkit and protocol to build GUI on nearly all Linux systems
#### ** 7. Desktop Environment
GUI on top of operating system, example, `GNOME, KDE, Xfce, and Fluxbox`
#### ** 8. Command Line
Interface for typing commands on top of the OS
#### ** 9. Shell
Command line interpreter than interprets the command line input and instructs the OS to perform any necessary tasks and commands, example, `bash, tchsh, and zsh`

## * Linux Distributions
The kernel is the brain of OS, but there are other components that build together Linux system. Bringing them together, testing for compatibility, and make them easy to install and update are the role of Linux Distribution. Distributions differ in which kernel version they use.

Some distribution backport improvements, means they copies some small bug fixes from new versions to old system, but backport can't add big new functions.

[Major Distribution Lists](https://distrowatch.com/dwres.php?resource=major)

![[linux-distribution-families.png|343]]

#### ** Linux Distribution Options and Considerations
1. Stability, long-term support
2. Cutting-edge software and ease of use: Ubuntu, Fedora
3. Free: RHEL, CentOS Stream, Alma Linux, Rocky Linux
## * Other Essential Tools and Applications in OS
#### ** Compilers
used to build software (translate human-written code to machine code)
#### ** Debuggers
to test and troubleshoot programs
#### ** Core Libraries
pre-written, essential shared code bundles, they are borrowed instead of rewriting basic functions from scratch
#### ** Graphic Systems
allow programs to display visuals on screen
#### ** Package Managers
make it easy to install, update, or remove software