### Questions

**Boot process (most of the time here)**

1. Put these in order: kernel starts, POST, bootloader menu, login prompt, `systemd`, BIOS/UEFI, `initramfs`. 🎯
2. How does BIOS/MBR find the bootloader, compared with UEFI? 🎯
3. Why is `initramfs` needed? What problem does it solve? 🎯
4. What is PID 1, and what is `/sbin/init` a symlink to? 🎯 What did it replace, and why is the new one faster? 
5. Write the `systemctl` commands to: start a service now, make it run at every boot, and check its status. What’s the difference between `start` and `enable`? 🎯
6. Which of these need `sudo`: reading `/etc/hosts`, editing a file in `/etc/`, installing software, checking service status, changing your own password?
7. How do you switch to a text terminal (TTY) and back to the graphical one? 🎯


**Installation**  
8. Name the 3 installation methods and one downside of each.  🎯
9. Desktop, server, and minimal/netinstall images: which would you pick for learning in VirtualBox, and why? 🎯

**Filesystem**  
10. What is the difference between a partition and a filesystem? What does “mounting” do? Give a mount point example. 🎯 
11. Primary vs extended partition: what is the limit, and why does the extended one exist?  🎯
12. Are `/boot` and `/Boot` the same directory in Linux? Where would a USB drive labeled `FEDORA` appear for user `student`? 🎯

### Answer key

1. BIOS/UEFI, POST, bootloader menu, kernel starts, `initramfs`, `systemd`, login prompt.
2. BIOS/MBR reads the boot order from CMOS, checks each drive in that order, and launches the bootloader it finds. UEFI uses its Boot Manager’s saved entries (disk, partition, path) and jumps straight to that partition to run GRUB.
3. The kernel needs disk drivers to mount the root filesystem, but those drivers are stored in that same filesystem. `initramfs` provides basic drivers in RAM so the kernel can reach and mount the real disk.
4. PID 1 is the parent of all processes. `/sbin/init` is a symlink to `systemd` (`/usr/lib/systemd/systemd`). It replaced Sysvinit, which loaded one program at a time with runlevels. `systemd` starts services in parallel and uses simple `.service` files.
5. `sudo systemctl start name`, `sudo systemctl enable name`, `sudo systemctl status name`. `start` runs the service now only, while `enable` makes it start automatically at boot. They are independent, so you can do either one without the other.
6. Needs `sudo`: editing `/etc/`, installing software. No `sudo`: reading system files, checking status, changing your own password.
7. `Alt+F-key` switches between terminals. `Ctrl+Alt+F-key` leaves the graphical environment, and `Ctrl+Alt+F1` or `F7` returns to it.
8. Virtual machine (needs extra RAM/CPU and 20 GB+ disk, and can be slower). Live media (slower startup, reduced performance, starts from scratch each time). Native install (risk to existing data, plus partition planning and UEFI Secure Boot complications).
9. Desktop image. It has a GUI and daily tools, is beginner-friendly, and works well in VirtualBox. Server images are command-line only, and minimal images mean installing everything yourself.
10. A partition is a fixed section of the disk. A filesystem is the logical structure that formats it. Mounting attaches a partition to a folder, for example `/dev/sdb1` mounted at `/home`, so everything joins into one tree.
11. Up to 4 primary partitions. An extended partition is a container you can split into many logical partitions when you need more than 4.
12. No, Linux is case-sensitive, so they are three different directories if all exist. The USB file would be at `/run/media/student/FEDORA/`.