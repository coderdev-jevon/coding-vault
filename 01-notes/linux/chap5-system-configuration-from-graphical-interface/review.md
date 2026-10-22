### Questions

**Package management (the core of this chapter)**

1. What is a package, and what does it contain? 🎯
2. What is the difference between a low-level and a high-level package manager? Name the pair for the Debian family and for the RPM family. 🎯
3. What file formats do the two families use? Why can’t you install a `.rpm` directly on Ubuntu? 🎯
4. What does `sudo apt update` do? Does it install new versions of your software? (Think about what an “online repository” and “metadata” are.) 🎯
5. What is a dependency, and which tool resolves them for you: `apt` or `dpkg`? 🎯
6. Snap vs `apt`: give two differences. 🎯
7. Which high-level package manager would you use on Fedora/RHEL? On openSUSE?

**Time and network**  
8. What time standard does Linux use internally, and what does your time zone setting do? Why does this matter for servers and clusters?  
9. What is NTP for? Name two programs that implement it.  
10. When you plug in a wired connection, how does NetworkManager configure it by default? Name the two terminal tools for NetworkManager.

**Bonus (VM, 1 minute):** run `timedatectl` and `dpkg -l | wc -l`. Which questions do the results relate to?

### Answer key

1. A self-contained bundle of program files, configuration files, documentation, and metadata.
2. A low-level manager unpacks files and places them in the right locations. A high-level manager builds on it, talks to online repositories, downloads packages and their dependencies, and offers a GUI and command line. Debian family: `apt` (high) and `dpkg` (low). RPM family: `dnf` (high) and `rpm` (low).
3. Debian family uses `.deb`, and the RPM family uses `.rpm`. Packages are built specifically for each distribution and version, so they aren’t interchangeable.
4. It connects to the online repository (the software catalog) and refreshes the local metadata about available packages and versions. It does not install or upgrade anything. That’s done by `sudo apt upgrade` or `sudo apt install name`.
5. A dependency is another package that a package needs in order to work. The high-level manager (`apt`, `dnf`) finds and downloads them. `dpkg` only unpacks the file you give it.
6. Snaps are self-contained, with all libraries inside the package, and update automatically. `apt` packages share libraries with the rest of the system. Snaps can coexist with `apt` versions of the same app.
7. `dnf` for Fedora/RHEL, and `zypper` for openSUSE (which also has the YaST graphical module).
8. UTC. Your time zone setting adjusts how the time is displayed to you. This matters because logs and jobs across many machines all share one reference time, which makes timestamps comparable.
9. NTP (Network Time Protocol) lets the machine query a time source to keep its clock accurate. Implementations are `systemd-timesyncd`, `chrony`, and `ntpd`.
10. It detects the connection automatically and configures it with DHCP. You can also enter a static IP manually. The terminal tools are `nmcli` and `nmtui`.

**Bonus:** `timedatectl` shows the time zone and whether NTP sync is active (questions 8 and 9). `dpkg -l | wc -l` counts installed `.deb` packages (questions 1 to 3).