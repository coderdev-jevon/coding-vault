# Chap 7: Working with Files
Date: 2026-08-20

## ==* Working and Managing Files==
```bash
cat # view file
	cat -n
tac # view file backwards in terms of lines
less 
	less -N
tail
head
	head -20 # 20 lines
wc # word count
```

#### ** `touch`
`touch` is often used to access, change, and modify times of files, but it can be use to create new empty file.
```bash
touch <filename> # create empty file
touch -t [[CC]YY]MMDDhhmm myfile # set file timestamp to 
```

#### ** `mkdir`and `rmdir`
```bash
mkdir sampdir # make sampdir under current directory
mkdir /usr/sampdir # make sampdir under /usr

rmdir # remove directory, directory must be empty
rm -rf # recursive force, remove directory and all of its contenects
```

#### ==** Moving, Renaming, Removing a File==
```bash
mv # it can rename a file or move a file, directory also
	mv source destination
	mv source1 source2 destination # move multiple files

rm
rm -f # forcefully remove a file
rm -i # interactively remove a file

cp # for copying
```


#### ==** Look for ONLY File or Folders with ..==
```bash
ls -l *file* # * means 0 or more
ls -l *dir*
```


## ==* Modifying Command Line Prompt==
**PS1 (Prompt String 1)** is your primary prompt string, like `jal@ubuntu:~$`.

```bash
PS1 = "\u@\h:\w \$ "
# user
# hostname (computer name)
# current working directory
# $ for normal users, # for root user
```

## ==* Standard File Streams==
It is basically just a data flow, file streams are pipes.

There are **3 built-in open file streams**:
1. 0 `stdin` (standard input) -> input stream
2. 1 `stdout` (standard output) -> normal program output
3. 2 `stderr` (standard error) -> error/warning message

## ==* I/O Redirection==

```bash
do_something < in.txt

command > out.txt # normal command to take output
#output goes to file, error message goes to screen

command 2> err.txt # command to take error message
#error message goes to file, output goes to screen

command > all.txt 2>&1 # output and error message into one file
command >& all.txt
```

## ==* Pipes==
```bash
command1 | command2 | command3
```
This is called as pipeline

Doing this allowed processing to be done faster, no need to save output of a program before continuing to the other.

## * Searching for Files
#### ==** `locate`==
locate scans pre-built database file on system not your hard disk live.
```bash
locate zip | grep bin

# always refresh database by
sudo updatedb
```

==`grep`== is a filter tool that read lines of text, take text coming from pipe or files.

```bash
grep -H cat pet.txt pet1.txt # look for "cat" inside pet.txt and pet1.txt

# -H means always show filename
# -h means heide all filenames
```

#### ** `/etc/updatedb.conf`
This is configuration file for `updatedb` which folders / filesystems to SKIP (prune), PRUNEPATHS for folders path to skip, PRUNEFS for file systems, and PRUNENAMES for folder names.

## ==* Wildcards==

```bash
? # match any single character
* # match any string of characters
[set] 
[!set] # match any character outside the set
```

```bash
ls ba?.out # ba something .out
*.out # bla bla bla .out

```

#### ** Install `vmware` right way
```bash
sudo apt-get install vmware* # X
sudo apt-get install "vmware*" # V
```

Why the second is correct not the first. Double quotes turn off glob expansion, so bash shell does not look at all files inside current folder, instead, it only search for package names.


## ==* `find`==
scan disk live, slower than locate but always up to date
```bash
find where-to-start -type [dlf] -name "pattern" -maxdepth 1 -ls
# d is directory, l is link, f is regular file

find . -name "test"
find /usr -type d -name gcc
```

#### ==** `find` and execute command==
```bash
find -name "*.swp" -exec rm {} ';' # Find files with the name and execute remove
# always end with ';' or \;

# OR
find -name "*.swp" -ok rm {} \; # for interactive purpose
```

#### ==** `find` based on time==
```bash
# BASED ON DAYS
find where-to-start -ctime 3 # inode metada last changed
find where-to-start -atime 3 # last accessed
find where-to-start -mtime 3 # last modified
+3 more than three days
-3 less than three days

# BASED ON MINUTES
find where-to-start -cmin 3
find where-to-start -amin 3
find where-to-start -mmin 3
```

#### ==** `find` based on size==
```bash
find where-to-start -size N[ckM] -exec command {} \;
# c for bytes, k for kilobytes, M for megabytes
```