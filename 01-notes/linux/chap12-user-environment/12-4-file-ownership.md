# Chap 12.4: File Ownership
Date: 2026-10-06

## ==* File Ownership==
In Linux and other UNIX-based OS, every file is associated with user or group.

```bash
chown # use to change user ownership of file or directory
chgrp # use to change group ownership
chmod # use to change permission on the file
```
## * File Permission Modes and `chmod`
Three kinds of permissions: read, write, execute (`rwx`)
Three groups of owners: user, group, others (`ugo`)

```bash
rwx: rwx: rwx
u  :   g:   o
```

```bash
ls -l somefile # checkpermission
```

#### ==`chmod` syntax 1==
```bash
chmod uo+x,g-w somefile
```

```bash
+ # add a certain permission
- # remove a certain permission
= # sets it exactly
```

#### ==** How to Read Permission==
```bash
-rwxr--r-x

- # file type
  rwx # can read, write, execute
  r-- # read only
  r-x # can read and execute
```

#### ==** Digit for Permission Bits==
```bash
4 # read 
2 # write
1 # execute
7 # read/write/execute
6 # read/write
5 # read/execute
```

#### ==** `chmod` syntax 2==
```bash
chmod 755 somefile
```

## ==* Example of `chown`==
```bash
sudo chown root file2 # change owner of file2 to root
ls -l file? # check the owner

sudo chown root:root file2 # change both group and owner to root
```

## ==* Example of `chgrp`==
```bash
chgrp groupname file

```
