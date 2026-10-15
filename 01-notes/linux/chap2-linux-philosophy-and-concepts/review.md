### Questions

1. Who developed the Linux kernel, and what license is it under?
2. In your own words, what does the kernel do? What is a distribution?
3. Why can Linux “treat everything like a file”? Give the example from your notes.
4. Linux is described as multitasking and multiuser. What does each word mean, and what is a daemon?
5. Name 3 examples of services (background programs). 🎯
6. What is a boot loader? Name two examples.
7. Name 4 file system types. 🎯
8. What is the difference between the shell and the command line? Name two shells. 🎯
9. What is the difference between a desktop environment and the X Window System? Name two desktop environments. 🎯
10. What does a distribution’s “backporting” mean, and what can’t it do? 🎯
11. What are the three things a distribution does besides including the kernel? 🎯
12. Match each tool to its job: compiler, debugger, core library, package manager.

**Bonus (VM, 1 minute):** run `echo $SHELL` and `uname -r`. Which question above does each answer relate to?

### Answer key

1. Linus Torvalds. It’s licensed under the GPL (General Public License), which let a worldwide community of developers contribute.
2. The kernel is the core of the OS, the glue between hardware and applications. A distribution is the kernel combined with other programs and software into a complete OS.
3. Linux uses file-like interfaces for many things. In your notes, even network connections are managed with the same utilities as regular files.
4. Multitasking means running many tasks at once. Multiuser means several users can use the system at once. A daemon is a background service process that handles system and network tasks.
5. Any three of `httpd`, `nfsd`, `ntpd`, `ftpd`, `named`.
6. A program that boots (starts) the operating system. Examples are GRUB and ISOLINUX.
7. Any four of ext3, ext4, FAT, XFS, NTFS, Btrfs.
8. The command line is the interface where you type commands. The shell is the interpreter that reads them and tells the OS what to do. Examples are bash, tcsh, and zsh.
9. The X Window System provides the standard toolkit and protocol for building GUIs. A desktop environment is the GUI built on top of it. Examples are GNOME, KDE, Xfce, and Fluxbox.
10. Backporting copies small bug fixes from newer versions into an older system. It can’t add big new features.
11. It brings the components together, tests them for compatibility, and makes them easy to install and update. Distributions also differ in which kernel version they use.
12. A compiler translates human-written code into machine code. A debugger tests and troubleshoots programs. Core libraries are pre-written shared code reused instead of rewritten. A package manager installs, updates, and removes software.

**Bonus:** `echo $SHELL` shows your default shell (question 8), and `uname -r` shows your kernel version (questions 2 and 10).