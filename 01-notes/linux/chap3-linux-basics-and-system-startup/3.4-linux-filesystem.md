# Chapter 3: Filesystem
Date: 2026-08-12

## * Filesystem Types
Linux filesystem is like a library, it is versatile (easy to adapt), it is categorized by genre, media type, and frequency of use

#### ** Conventional Disk Filesystems
This is regular SSDs and hard drives, example: ext4, XFS, `Btrfs`

#### ** Flash Storage Filesystems
Used for raw flash memory (like those in embedded devices), example: UBIFS, YAFFS

#### ** Special Purpose Filesystems
Do not live in hard drive/SSD, they live in RAM, appear as `/proc, /tmp, etc`

#### ** Database Filesystems
Not like standard filesystem, it treats data as objects or rows within a database, designed for high-speed searching, metadata richness, and data integrity.

## * Partition and Filesystems
#### ** Physical Storage vs Logical Organization
Physical storage is the tangible storage space, hard disk, SSD, etc. While logical organization, is software rules to manage data, disk partitions, filesystem type, etc.

#### ** Partition and Filesystem Definition
You can treat partition as a fixed area to be managed by a single unit. Filesystem is the logical structure that format the partition.

#### ** Mounting Connects Everything into Continuous Folder Tree
Partition is a separate storage box, to connect partitions together, you need to pick mount point for each of the partition, for example `/dev/sdb1` as `/home`, ... as `/`, at the end all connects together.

#### ** Windows vs Linux Storage Concepts
![[linux-windows-storage-concepts.png|352]]

## * Filesystem Hierarchy Standard
FHS: How Linux decide where things to go, standard evolves overtime and you may encounter minor differences between distributions.

#### ** Key FHS Top-Level Directories
![[linux-key-fhs-1.png|491]]
![[linux-key-fhs-2.png|493]]

#### ** Removable Media
Removable media is also accessed through filesystem tree, on modern Linux system, it is under `/run/media/yourusername/disklabel`

If your username is `student`, USB drive labeled `FEDORA`, and file `README.txt` stored there, then it will be under `/run/media/student/FEDORA/README.txt`

It is similar to `E:\README.txt` in Windows


#### ** Case Sensitivity
Linux treats uppercase and lowercase in filenames as complete distinct, `/boot`, `/Boot`, and `/BOOT` are three separate directories, while in Windows and macOS, they are case-preserving and case-insensitive. 

Always stick to lowercase letters for any file creation.

#### ** The `/usr` Directory
`/usr` originally stood for Unix System Resources, now it is understood as home of the OS's general-purpose software layer.

Everything user `/` is like tools a technician would need to repair system. Some directories might have counterparts in `/usr` like `/usr/bin`, `/usr/lib`, in today's system, they are linked to the same path

![[linux-usr-subdirectories.png|503]]