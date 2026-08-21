# Chap 7: Command  Basic Operations
Date: 2026-08-19

## ==* Basic Operations==
```bash
cd
cat
echo # print out text to your screen
ls
rmdir
man
exit # exit current shell process
login # mostly run on VTs, to login to another user
mkdir
```

## ==* Secure Shell (SSH)==
Local login allows your shell to run on your own computer, while SSH allows you to run shell on different computer over network. 

Remove machina can be public remote-server or private remote-machine.

Authenticate by password or cryptographic key (SSH key)

```bash
ssh student@remote-server.com
```

#### ** Why run shell on different computer
Many computers live in data center far away, by SSH, you can connect over network to control them.

#### ==** How to test SSH==
```bash
# First install ssh
sudo apt update
sudo apt install openssh-server

# Check if ssh service is running
systemctl status ssh
sudo systemctl start ssh

# Get VM's own IP address
hostname -I

# Test connect SSH
ssh jal@10.0.2.15

# Stop ssh
sudo systemctl stop ssh #or 
sudo systemctl disable ssh
```

`openssh-server` is server side for SSH, which contains `sshd`, service that listens for incoming SSH connection

## ==* Rebooting and Shutting Down==
```bash
shutdown # this prevents further users from login in and init process will control shutting down and rebooting

shutdown -h # shutdown halt (shut down)
shutdown -r # shutdown reboot
```
#### ** Scheduled Shut Down
```bash
# Absolute time
sudo shutdown -h HH:MM "message"
# Relative time
sudo shutdown -h +10 # 10 minutes from now
sudo shutdown -h +0 # 0 minutes from now
```

## * Locating Applications
Programs can be in `/bin, /usr/bin, /sbin, /usr/sbin, /opt, /usr/local/bin, /usr/local/sbin, home/student/bin`

#### ==** Locate Programs==
```bash
which appname 
whereis appname # look for package and man files
```

## ==* Accessing Directories==
`$HOME` is the path of home directory folder.
```bash
pwd # print working directory, display present working directory
cd ~ # ~ expands to folder path
cd # zero argument -> user value from $HOME
cd - # minus, change to previous working directory
cd .. # .. means one folder about current location

# Save directories onto directory stack
pushd ~/Documents # Add to the top of the stack
popd # Move back to top of the stack
```

## * Absolute vs Relative Paths
#### ** Paths
```
////usr//bin and /usr/bin are treated the same
```
#### ** Absolute pathname
It begins with / and follows the tree.

#### ** Relative  pathname
It starts from present present directory, never start with /.

You take advantage of `.` as present directory, `..` as parent directory, `~` as home directory

#### ==** Filesystem Tree==

![[linux-directories.png|414]]

## ==* Exploring Filesystem==
```bash
tree -d # directories
tree -L N # limit depth, show only N levels
tree -a # all, show all entries, including hidden files/folders
tree -f # absolute file path
tree -h # human-readable file sizes, show file sizes
tree -p # show file permission bits
tree -I "shell-glob-pattern" # Ignore, exclude items that match pattern
tree --noteport # remove final summary line

ls -a # list all files
```
#### ** Install `tree`
```bash
sudo apt update
sudo apt install tree
```

#### ==** Directory Levels==
```
/home/jal          ← Level 0 (starting point)
├─ Documents       ← Level 1
│  └─ notes        ← Level 2
└─ .ssh            ← Level 1
```

#### ==** `df`==
disk-free, check mounted partitions disk usage
```bash
-h # human readable (GB/MB)
-T # show filesystem type
-i # show inode usage
-x tmpfs # exclude memory-based tmpfs virtual filessytems
```

**`Inode`**, it is like ID card for each file which contains file size, permissions, owner, timestamp, disk block location, each filesystem has a fixed pool of  `inodes`.
```bash
df -h # basic human readable
df -hT # human + filesystem type
df -hT -x tmpfs # real disks only, clean output
df -i / ## check inode on root filesystem
df -h /home # show info for /home's paritition
```

#### ==** du==
disk usage, calculate strong of every sub-directories
```bash
-h # human-readable
-s # summary, only show total for targetted directory
-d N # depth limit
--apparent-size # show logical file size
```

```bash
du -sh . # show summary in human-readable size of current directory
du -sh * # every single item inside current directory
du -h -d1 /home/jal # show size of immediate childer folders
```

## ==* Hard Links==
`ln`, link,  makes links, pointer to a file
```bash
ln file1 file2 # both files share the same inode, any edit on either file will affect the other file
```

`.` and `..` belong to hard links.
#### ==** Soft / Symbolic Link==
does not take extra space
```bash
ln -s file1 file3 # file3 is just a shortcut, they share different inode
```

**dangling link**, it is a link to currently not available object. 
#### ** What differs them
Delete file1 will not affect file2, while deleting file1 causes file3 as the shortcut to be broken, `symlink` is broken.

#### ** `ls`
list, list contents of a directory
`ls` is for Linux, `dir` is for Windows
```bash
-l #long format
-a # all, show hidden dot-files
-i # show inode number
-h # human-readable file sizes
-t # sort by modification
-r # reverse sorting order
-R # recursize, list all sub folders
```

#### ** `dirs`
when you used `pushd` and `popd`, `dirs` shows you where you have been.
