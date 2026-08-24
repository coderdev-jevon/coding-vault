# Chap 7: Installing Software
Date: 2026-08-21

## ==* Package Management System==
Consists of low-level tool (such as `dpkg` or `rpm`) and high-level tool (such as `apt`, `dnf`, or `zypper`).

Low-level: unpacking packages, running scripts
High-level: download packages from vendor, figuring out dependencies

![[linux-package-management-two-levels.png|444]]


## ==* `dpkg`==
```bash
dpkg --list | grep bolt # look from all of the lists in dpkg package manager, and look for bolt package

dpkg --listfiles bolt | less # look for files inside bolt package

sudo dpkg --remove bolt # remove bolt package, keep config files
sudo dpkg --purge bolt # remove everything, including config files

```

## ==* `apt`==
```bash
apt-cache # used for query or search information
apt-cache search firefox # search
	apt-cache search --names-only dump # only look for names, not descriptions
apt-cache show firefox # show full details
apt-cache policy firefox # show available versions and which one will be installed

sudo apt-get install firefox # can be used for upgrade installed package as well
sudo apt-get remove firefox
sudo apt-get update # only download latest metadata from repo
sudo apt-get purge firefox
sudo apt-get upgrade # system-wide upgrade
sudo apt-get dist-upgrade # system-wide full smart upgrade
```