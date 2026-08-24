# Chapter 3: Ubuntu Installation
Date: 2026-08-09

# Steps
1. Go to [virtualbox.org](https://link.wtturl.cn/?target=https%3A%2F%2Fvirtualbox.org&scene=im&aid=497858&lang=zh)
2. Download virtual box for windows (Windows hosts) and virtual box extension pack, version must match
3. Then run virtual box .exe file, run as administrator, don't change anything
4. Add extension pack to the virtual box
5. Download Ubuntu 24.04 from website, make sure the file size is around 6GB
6. Go to virtual box, create new, and fill in name as `Ubuntu_24.04` and add Ubuntu file to ISO image and next, unattended installation
7. Add password 123123
8. Adjust setting, base memory 2048MB for 8GB total RAM, drag slider to 2CPUs, Disk Size to 40GB to have enough space to install software later, tick use EFI,
9. Change settings Video Memory to 128 GB, max
10. Then start, click ctrl and right click if you want to release mouse/keyboard back to Windows
11. Try/Install Ubuntu and wait
12. Close welcome window and search for Install Ubuntu on left vertical sidebar
13. If you are not sure about you ubuntu `.iso` file, you can check the hash 256, is it the same
14. If error, no unattended installation, when entering GRHB after starting VM press E, add `nomodeset` at the very end of the line which starts with `linux`, then click `f10` to boot., you can also Try Ubuntu in safe graphics mode
15. Then click Install Ubuntu, follow with the steps according to your situation
16. After installation success, go to terminal and reboot by command `sudo reboot
17. If you forget root password, at the start of VM booting, press `Esc` multiple times to load a different menu, click menu with `root -> Drop to root shell prompt`, then run these commands `mount -o remount,rw /`, then `passwd [your_username]`, then type you new password, lastly to exit, write `reboot` or reboot by GUI.
18. 




## ** CentOS 9 Stream Installation Fast Overview
1. Download VM Ware and Open it after installation
2. Download CentOS 9 Stream `.iso` file
3. Create New Virtual Machin inside VM Ware, insert `.iso` file and follow with the procedures.