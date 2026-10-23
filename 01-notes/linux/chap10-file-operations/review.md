### Questions

**Mounting and storage**

1. Partition vs mount point: which is `/dev/sda1` and which is `/home`? What does `umount` do, and why does a manual `mount` vanish after reboot? Which file fixes that? 🎯
2. What does `df -Th` show? What is `tmpfs`, and why is it not a real disk? 🎯
3. What is NFS (Network File System), and why is it useful on a cluster of GPU machines? Which file on the server defines the shares, which command applies changes, and what does the client run to attach a share? 🎯

**Layout (what lives where)**  
4. `/proc`, `/sys`, and `/dev`: what does each hold? What is a “virtual file”? Give two `/proc` files you could read to check a machine’s CPU and memory.  🎯
5. What is `/var` for, why must it survive reboot, and which subfolder do you check first when a job fails?  🎯
6. Where would each go: system config files, software you compiled yourself, commercial software installed manually?  
7. Name the four kinds of files in `/boot`. What lives in `/lib/modules`, and how does that relate to GPU drivers? 🎯

**Backup and compression**  
8. `cp` vs `rsync`: why is `rsync` better for backups? What do `-a`, `-v`, `--delete`, and `--dry-run` do? Why run `--dry-run` first?  🎯
9. Write the commands to create a gzip-compressed archive of `mydir` and to extract it. What do `c`, `x`, `z`, `v`, `f` mean? Why does `tar` come before compression?  🎯
10. Compare `gzip`, `bzip2`, and `xz`: speed, size, extension. Which command measures how long one takes?  🎯
11. What does `dd` copy that `rsync` doesn’t? What do `if`, `of`, `bs`, `count` mean? Why is `dd` dangerous, and what do you run first?  🎯
12. What are `diff -u` and `patch` for? What does `file` tell you that the extension doesn’t? 🎯

**Scenario**  
13. A training run crashes with “No space left on device.” Give the commands, in order, to find which partition is full, then which folder is using the space, and one way to free it up safely.

**Bonus (VM, 1 minute):** run `df -hT -x tmpfs`, `head -5 /proc/meminfo`, `ls /boot`, and `time tar czvf test.tar.gz ~/Documents`. Which questions do they relate to?

### Answer key

1. `/dev/sda1` is the partition (a device node), and `/home` is the mount point (a folder). `umount` detaches the partition, and `/home` goes back to being an empty folder. Manual mounts live only in the running system, so they’re lost on reboot. Add an entry to `/etc/fstab` to make it permanent.
2. It lists mounted filesystems with type, size, used, and free space in human-readable form. `tmpfs` is a temporary filesystem stored in RAM, not a real partition, used for temporary runtime data.
3. NFS lets machines mount a folder from a server so everyone sees the same files. On a cluster, all GPU nodes can read the same dataset and write to the same checkpoint folder without copying. Server: `/etc/exports`, applied with `sudo exportfs -r`. Client: `sudo mount SERVER_IP:/srv/my_share /mnt/nfs_client_share`.
4. They are virtual files, not stored on disk. The kernel generates the content when you read them. `/proc` holds live kernel and process info, `/sys` holds hardware devices and kernel modules, and `/dev` holds device nodes that programs use to talk to hardware (created by `udev`). `cat /proc/cpuinfo` and `cat /proc/meminfo`. GPUs also appear as device nodes (like `/dev/nvidia0`) once their driver loads.
5. `/var` holds system files that change in size and content (logs, caches, databases, queues). It lives on disk and survives reboot. Check `/var/log` first.
6. Config files go in `/etc`, self-compiled tools in `/usr/local`, and manually installed commercial software in `/opt`.
7. `vmlinuz` (compressed kernel), `initramfs`, `config`, and `System.map`. `/lib/modules` holds kernel modules, mostly device drivers, which can be loaded and unloaded without rebooting. 
8. `rsync` copies only what changed and skips unchanged files, and it can copy to another machine directly. `-a` is archive mode (keeps properties), `-v` is verbose, `--delete` removes files in the destination that no longer exist in the source, and `--dry-run` shows what would happen without doing it. Run the dry run first because `--delete` can destroy data if you swap source and destination.
9. `tar czvf mydir.tar.gz mydir` and `tar xvf mydir.tar.gz`. `c` is create, `x` is extract, `z` is gzip, `v` is verbose, `f` is the archive file name. `tar` bundles many files into one archive, and the compression tools then shrink that single file.

	`tar` stands for tape archive
10. `gzip` is fast and common (`.gz`), `bzip2` gives smaller files but is slower (`.bz2`), and `xz` is the smallest and slowest (`.xz`). `time command` measures the duration.
11. `dd` copies every byte of the raw device, including empty space, the boot area, and deleted data still in blocks, while `rsync` copies files only. `if` is input, `of` is output, `bs` is block size, `count` is how many blocks. Swapping `if` and `of` can overwrite a whole disk, so run `lsblk` first to confirm which device is which.

	`dd` stands for data definition

12. `diff -u` shows what changed between two files, and `patch` applies those changes to another copy (how source code changes are shared). `file` reports the real type of a file from its contents, since Linux doesn’t trust extensions.
13. `df -h` (which partition is full), then `du -sh *` or `du -h -d1 /path` (which folder is big). Free space safely by deleting old checkpoints you’ve confirmed you don’t need, or by compressing or moving them (`tar czvf`, then `rsync` to another machine). Check twice before deleting.

**Bonus:** `df -hT -x tmpfs` relates to questions 1 and 2, `/proc/meminfo` to 4, `ls /boot` to 7, and `time tar czvf` to 9 and 10.

