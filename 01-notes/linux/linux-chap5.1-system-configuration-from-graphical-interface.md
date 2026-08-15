# System Configuration from the Graphical Interface
Date: 2026-08-13

Configuration - how parts are set up to make a whole.
Configuring - setting up or arranging parts of something to work in specific way.

**Objectives**:
- Adjust system, display, and date and time settings using Settings panel
- Manage network connections using Network Manager
- Install, update, and remove software using graphical package management tools

## * System, Date and Time Settings
#### ** GNOME Tweaks
Gnome tweaks is advanced customization for Linux, use it if you want to change how the desktop looks and behaves.

To install GNOME Tweaks, follow this
```
sudo apt update #apt is a built-in package manager to install
sudo apt install gnome-tweaks
gnome-tweaks #open the app
```

You may run a command by `alt + F2`
`alt` means alternate key, triggers alternative function
#### ** Date and Time Settings
Linux uses Coordinated Universal Time (UTC), derived from UTC and adjusted by your configured time zone.

Clock in the top bar can be clicked to open calendar and notifications.

Automatic Date and time allows Linux to use Network Time Protocol (NTP) to query info to time. Examples of NTP are `systemd-timesyncd, chrony or ntpd`

## * Network Configuration
#### ** Network Manager
Experienced administrators do work with files containing network configuration directly, but you are not. You use Network Manager GUI to manage network connection.

Network manager helps you to manage full range of connection types, like wired Ethernet, Wi-Fi, mobile broadband, and VPN, also manage connection profiles.

Wired Ethernet - Network Manager detects connection automatically and configures it by DHCP (Dynamic Host Configuration Protocol), apart using this, you can enter specific IP address, ...., manually.

Each hardware has its own MAC address, virtual box as well, it is used as a unique identifier for routers.

## * Installing and Updating Software
#### ** Packages Definition
It is self-contained bundles that include program files, configuration files, documentation and metadata. Every component of Linux system is managed as a package.

## ** Package Manager
Linux packages depend on other packages to function.
1. Low-level package manager -> unpacking files and placing them in correct locations
2. High-level package manager (builds on top of low-level) -> communicates with online repositories, download packages and dependencies, also provide GUI and CL.

High-level package manager like `apt` and `dnf` connects to online repository (like Microsoft Store), download its latest metadata (software catalog) and save it to ubuntu disk.

Each packages are built specifically for each distribution and version, not interchangeable.

#### ** Debian Family
Format: `.deb`
High-level package manager: `apt`
Low-level package manager: `dpkg`

#### ** RPM Family
Format: `.rpm`
RHEL/Fedora: `dnf`
openSUSE: `zypper` -> openSUSE provides `YaST` Software Management module, which is feature-rich in graphical.
Low-level package manager: `rpm`

#### ** Snap Packages
It is independent package format created by Canonical. If APT is like renting an apartment in a shared building. Snap app is self-contained tiny mobile home, auto update, all libraries is inside the package, does not rely on shared files, and coexist alongside APT packages.

You may have two same apps, one is installed via `apt` and the other is installed via snap package.


#### ** Download GNOME Software App
```
sudo apt update
sudo apt install gnome-software

```

#### ** Synaptic Package Manager
Use this for advanced control purely for APT /`.deb` packages