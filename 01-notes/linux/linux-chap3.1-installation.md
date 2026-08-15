# Chapter 3: Linux Basics and System Startup
Date: 2026-08-06
│
├── Installation
│   ├── Distribution concepts       🟢
│   ├── Installation methods        🟡
│   ├── Ubuntu installation         🟢
│   └── CentOS installation         🔴
│
├── Boot Process
│   ├── Boot overview               🟡
│   ├── BIOS/UEFI                   🟡
│   ├── MBR/EFI                     🟡
│   ├── Bootloader                  🟡
│   ├── initramfs                   🟡
│   ├── Kernel                      🟢 concept
│   └── systemd/services            🟡
│
└── Filesystem
    ├── Filesystem types            🟢
    ├── Partitions/filesystems      🟢🟢
    ├── FHS                         🟢🟢
    ├── Filesystem hierarchy        🟢🟢
    └── GUI navigation              🔴

Goal for this chapter:
1. Identify Linux filesystems
2. Identify differences between partitions and filesystems
3. Describe the boot process
4. Install Linux on a computer

## * Information about Switching Distribution
Material produced by Linux Foundation is distribution-flexible, by playing around management systems, software versions, and file locations, switching will be painless

## * Installation Media
1. **UBS flash drive**, write system files to USB drive, plug into new PC, and boot from it, then install Linux/Windows 
2. **DVD disc**, traditional installation media, burn system image onto DVD
3. **ISO image**, single archive file containing all installer data, bootable USB/DVD

system image - a complete file that packages the entire state of OS, can be ISO image or Backup/clone image

#### ** What to consider when downloading ISO image
1. **Architecture**, it implies the instruction set your processer uses, OS binary must match your CPU (brain of computer), standard modern laptops use 64-bit images.
2. **Image package content**, what built-in files, tools, and desktop environment available inside the image
	- **Desktop image**, with GUI, web browser, media tools, daily apps
	- **Server image**, no GUI, only command line
	- **Minimal/`netinstall` image**, only basic core system, manually install everything later, usually requires less time in initial downloading, but take longer overall.
#### ** How it is working
1. New computer has no OS
2. Boot computer from installation media
3. Installer loads up, guide to format the hard drive and install the OS
## * Installation Methods
#### ** 1. Virtual Machine
- Runs Linux inside existing OS, runs as a guest OS inside program called hypervisor, main OS remains the host system.
- Downside: requires additional memory and CPU resources, also at least 20 GB of disk space and performance might be slower than directly on hardware
[virtual box](https://www.virtualbox.org/)
[VMware player](https://www.vmware.com/)
#### ** 2.  Live Media
- Linux distributions provide live USB or DVD to run Linux without installing it on hard drive, Linux runs directly on removable device
- Good for testing compatibility, after doing it, you can usually start a full installation
- Downside: startup time can be slower, always initializes from scratch each time, performance is reduced compared to full installation

#### ** 3. Native Installation
- Install Linux directly on computer's hardware, provide the best performance
- Dedicated installation, fully replace existing OS, or Multi-boot installation, installed alongside another OS, choose what OS to boot at the start
- Require considerations on size of disk space, size of disk partitions, or loss of existing data might occur, always consult to installation documentation
- Another complication is UEFI (Unified Extensible Firmware Interface) Secure Boot, in which it prevents non-approved OS from booting

## * Pre-Installation Checklists
![[linux-pre-installation-checklists.png|329]]

#### ** Backup Your Data
These two steps are not so important while you use virtual machine as your installation method, backup data can be through `Google Drive`.

#### ** Check Hardware Compatibility
Before committing full installation, it's recommended to test using Live Media, test Wi-Fi or network connectivity, Audio and speakers, Keyboard and mouse or trackpad, Display resolution and graphics performance, Webcam and other peripherals.
#### ** Verify Architecture
`Right click This PC -> Properties -> Look at System type`
#### ** Always watch demo first
How to install `[distro name]`

## * Choose the Right Distribution
Linux ecosystem provides a variety of choices, starting from the general-purpose server to highly specialized embedded distributions.

![[linux-distribution-choices.png|364]]

#### ** Desktop Linux
Best for students, new Linux learners, daily computer use
**Pros**:
1. Beginner-friendly: intuitive GUI, simple installation, massive tutorials
2. Complete daily tools
3. Perfect for VirtualBox
4. Flexible: can turn this desktop system into lightweight server by removing graphical interface

**Cons**:
1. Extra background programs consume RAM/CPU
2. Regular automatic updates bring minor desktop bugs
3. Require around 20 GB of storage

#### ** Server Linux
Best for building websites, cloud servers, network hosts
**Pros**:
1. Ultra-stable and secure, Minimal extra software, fewer bugs and security vulnerabilities
2. Low resource usage, saves RAM/CPU
3. Long official support cycle (5-10 years) which make it reliable for long-term operation
4. Might fit under 2 GB of storage

**Cons**
1. Everything is done by typed commands only, confusing for beginners
2. No daily convenient tools, manually install every app you want
3. Slow software updates, latest software is delayed

#### ** Embedded Linux
Best for hardware development, IoT(Internet of Things) engineering
**Pros**:
1. Extremely lightweight, requires very minimal storage
2. Ultra-low power consumption, highly customized for specific hardware

**Cons**:
1. Very advanced and complex
2. Not for general use
3. Very few beginner learning resources

## * Partition
Hard drive/SSD (Solid State Drive) is just one big blank physical storage plate, a partition is splitting this large disk into several independent, separated logical sections.

#### ** Windows way
Use drive letters, C: for windows system, D: for games and files

#### ** Linux way
/ is the global root, partition A mounted at /, stores core OS system files, partition B mounted at /home, stores personal photos and documents, partition C mounted at /boot, stores files needed to boot Linux

#### ** Two Types of Partitions
1. **Primary Partition**, only max of 4 primary partitions that can hold OS and be used to boot the computer
2. **Extended Partition**, a special empty container partition, you can split it into many small logical partitions, use this if you need more than 4 partitions in one Disk

## * Additional Software to Include during Installation
1. **Desktop Environment**, GUI such as GNOME or KDE Plasma
2. **Productivity Applications**, web browsers such as Firefox, media players, office suites like Microsoft Office and LibreOffice
3. **Development Tools**, text editors, compilers, version control tools such as Git
4. **Server Software**, Apache web server or MySQL database

## * Security Setup
**Mode A "Separate Password for Root**: log in as regular user normally and when you need high authority, switch to root account by entering root password

**Mode B "User Admin Privileges"**: never log in into root directly, when you need administrator power, add command `sudo` before instruction, then input regular user password


## ** Automated Installation
If a company needs Linux installed on 100 office computers, manual setup for username, password, partition settings, step by step, is slow. So people make pre-written answer file, that loads together with Linux installer.

![[linux-automated-installation.png|331]]

## * Installation Process
1. Boot from installation media, you may be presented with options like starting installation directly, booting into live environment, or running a memory test.
2. Configuration questions: language, keyboard layout, time zone, network configuration, partition layout, user account creation, and software selection
3. Installation: format partitions, copies OS files, install selected packages, and configures bootloader
4. Updates: option to apply available updates or separate update step after the first boot
5. Reboot and first boot, some may do process accepting license agreement or completing account setup.

## * Linux Boot Process
Procedure to initializing the system, process from first switched on to fully operational

#### * The first step: BIOS
![[BIOS.png|142]]

![[BIOS2.png|154]]
Basic Input/Output System initializes screen and keyboard and tests the main memory, also called as POST, Power On Self Test. BIOS stores on RAM chip on the mother board. The rest of the process is controlled by OS.

Boot Loader is stored inside MBR system traditionally or EFI partition with UEFI (Unified Extensible Firmware Interface) firmware.

Boot Loader, example, GRUB (Grand Unified Boot Loader), ISOLINUX, for booting from removable media, Das U-Boot, for booting on embedded devices/appliances.




#linuxinstallation #linuxboot