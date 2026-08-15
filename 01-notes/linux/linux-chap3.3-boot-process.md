# Chapter 3: Boot Process
Date: 2026-08-11

Objectives:
1. Understand what happens behind the scenes each time Linux starts
2. Learn to troubleshoot startup issues, improve system performance, and customize how system loads

## * Linux Boot Process
![[linux-boot-process.png|213]]

## * BIOS - The First Step
BIOS begins everything, performs POST (Power-On Self-Test) which initializes and checks if hardware like screen and keyboard works properly, lastly loads bootloader.

## * Master Boot Record (MBR), EFI Partition, and Boot Loader

![[linux-bios-uefi-boot.png|438]]
MBR can't contain bootloader because of file size restriction.

#### ** BIOS/MBR Way
Boot loader is stored in system storage device. After the first step, BIOS, receive information from CMOS about system date and boot order priority (which drive to check first for an OS), then BIOS use this order rule to start checking storage drive which contain bootloader. Lastly BIOS launch bootloader.

#### ** UEFI Way
UEFI firmware has its Boot Manager with saved entries, like which physical disk, which partition, and path to boot program. UEFI jumps straight to that partition and runs GRUB.


After BIOS or UEFI finished its task, the boot loader shows selection menu to choose desired OS or kernels. Then boot loader loads Linux Kernels and `initrd` (initial ram disk) or `initramfs` (initial filesystem) into RAM, then CPU runs the code in RAM.

After that, kernel `uncompress` itself, checks and analyzes system hardware, and initializing any built-in device drivers.

## * Initial RAM Disk
Kernel then faces technical limitation when mounting root filesystem to access system tools. Initial RAM Disk (`initramfs`) present here, as the driver required to talk to storage hardware is stored in that very filesystem, `initramfs` provide basic disk drivers to create early user space allowing kernel to detect, access, and mount the main hard drive.

## * Text-Mode Login
System then gained access after mounting the root filesystem. The init process starts multiple hidden text login screens, can be text mode or graphical mode (GNOME), after log in, you will be greeted by command shell.

#### ** Virtual Terminals (TTY)
In one Linux, you can have multiple sessions through TTY (workspaces), usually six text terminals and one graphical terminal, starting from `F1` or `F2`. 

Switch between TTY by `ALT` + `Function key (F1, F2)`
Switch from Graphical Environment `CTRL + ALT  + Function Key`
Return to Graphical Environment `CTRL + ALT + F1 / F7`

#### ** Command Shell
`bash` is the standard interactive login shell, `$ or #` indicates readiness of your input, `Enter` as trigger to execution of the task.

## * Linux Kernel
Kernel acts as the heart of OS. After kernel is active in RAM, it claim hard wares, functions like `start_kernel()` and `initcalls` bring hardware to life. Kernel maps system's physical RAM (memory management of OS and applications), identifies and initializes all CPUs to handle tasks simultaneously, and it finds all attached I/O for communication purpose. 


## * `Init` Process

#### ** `/sbin/init`
After kernel completes hardware setup and mount the root filesystem, it launches program `/sbin/init` or called as `init` process, it is parent of all processes (PID 1). It is symbolic link  or `symlink` or shortcut to `systemd` binary `/usr/lib/systemd/systemd`

Init process responsibilities include process initiation, system management, ongoing maintenance, and system shutdown.

Before `systemd`, `Sysvinit` is the old classic startup system which implemented sequential loading (on program at a time) and `runlevels` in which user should pick a mode (single-user-mode, multi-user-mode), it was slow and hard to manage.

#### ** `systemd`
`systemd` uses aggressive parallelization (multiple services at a time), declarative configuration (simple `.service` configuration files)

use `systemctl` command is primary tool to interact with `systemd` manager.

use `apache2` for Debian/Ubuntu and `httpd` for RHEL/Fedora to manage Apache web server services.

## * `systemd` commands
#### ** Real-Time Service Control
To change state of a service on currently running system
`systemctl` means system control
```
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
```

#### ** Boot-Time Configuration
To determine whether service should run automatically when computer turns on
```
sudo systemctl enable apache2
sudo systemctl disable apache2
```

#### ** Monitoring Service Health
To check if service is running, view its recent logs, or see its process ID (PID)
```
sudo systemctl status apache2
```

## * When to use `sudo` command
It is used if the action changes system-wide resources (affects the whole computer)
1. Install / remove software
2. Start, stop, restart system background services
3. Edit configuration files stored in `/etc/` (system config folder)
4. Modify disk mounting, network global settings
5. Change other user's password

#### ** When to not use `sudo` command
1. List files, create folders in own directory
2. Launch normal desktop applications
3. Check status of services
4. Read system files
5. Change your own password when already logged in