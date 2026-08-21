# Chap 7: Command-Line Mode Options
Date: 2026-08-15

There's a saying "GUI make easy tasks easier, while command line make difficult tasks possible." Linux System Administrators spend most of their time at command line prompt.

## * Command Line Advantages
1. You ==don't get extra system load from GUI==
2. ==Almost all tasks are possible== doing at command line
3. You can ==implement scripts== for often-used tasks and procedures.
4. You can get ==access to other computers far away.== 🤔
5. ==Search for applications directly== without scrolling through menus.
6. ==CLI is static== not vary like GUI.


## * Terminal Emulator
A ==terminal emulator is like old-style physical text-only terminal machine== but in form of GUI. Example: `gnome-terminal`, `xterm`, `konsole`, `terminator`

## * Launch Terminal
**First Way**: Right click anywhere and select "Open in Terminal"
**Second Way**: Hit `Alt + F2` and type `gnome-terminal`

## * Basic Utilities
- ==`cat`== (works best for text) -> concatenate
```bash
cat filename.txt # show all text inside the file
cat file1.txt file2.txt # combine multiple files on screen
cat file1.txt file2.txt > all.txt # combine multiple files into all.txt
cat > filename.txt # create new file, type `Ctrl + D` to send the text you wrote
```
- `less`
```bash
less filename.txt #show text page by page
# Space -> scroll down one page
# b -> back to previous page
# Arrow Up Down Key -> scroll line by line
# /keyword -> search for keyword
# Enter -> move down one line
# q -> quit
```
- ==`head`== -> show first few lines of a file
- ==`tail`==  -> show last few lines of a file
- ==`man`== ->  manual, use to view documentation

#### ** The Use of ==Pipe Symbol (|)==
```bash
man head | less # left produce output and right receives that output as input
```

## * The Command Line
A command line have three basic elements: ==command, options, and arguments==, not all three must exist in a command, line  only command is a must

Command -> program or script to execute
Option -> modifiers for command, start with one or two dashes, `-` `--`

There are other elements such as setting environment variables.

## * `sudo`
You use `sudo` to provide the user with administrative power.

==A **configuration file** is== plain text that stores settings for a program, it defines how a program behave.
#### ==** How to Setup `sudo`==
1. Type `su` at command line and `Enter`, different looking prompt will appear
2. Type `echo "student ALL=(ALL) ALL > /etc/sudoers.d/student"`
3. Lastly type `chmod 440 /etc/sudoers.d/student`
	==File name can be anything==

**Explanation**
`/etc/sudoers` is the main file that defines who are allowed to run `sudo`. You are allowed to add config files to `/etc/sudoers.d/`, the permission rule in this case is `username ALL=(ALL) ALL`

First all means all hosts/machines, second (ALL) means allowed to run commands as any user, and last ALL means can run every possible command.

#### ==** How to Make `sudo` to not require password==
```bash
echo "student ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/nopasswd
chmod 440 /etc/sudoers.d/nopasswd
```

#### ==** How if there are two Files for the same user==
```bash
# In file 1: /etc/sudoers.d/student
student ALL=(ALL) ALL

# In file 2: /etc/sudoers.d/nopasswd
student ALL=(ALL) NOPASSWD: ALL
```
Files inside this folder are read in alphabetical order, s comes after n, so s overwrites n.

Make the one you want win by
```bash
rm /etc/sudoers.d/student

#or

mv /etc/sudoers.d/nopasswd /etc/sudoers.d/99_nopasswd
```


==**Why you need to change mode?**==
A newly created file permission settings is too open, the default is 
`-rw-r--r--` or can be seen as `- rw- r-- r--` which is 644.

|First char|File type|
|---|---|
|`-`|regular ordinary file (text file, program, config file) ✅ what you saw|
|`d`|directory (folder)|
|`l`|symbolic link (shortcut)|
|`b`|block device (hard‑disk)|
|`c`|character device|

`chmod` means change mode.

`4` means read -> view content
`2` means write -> modify, edit
`1` means execute -> run as program
`0` means no permission at all
`6` means read + write
`7` means read + write + execute

```bash
chmod u=r,g=r,o-rwx /etc/sudoers.d/student
# u means user (owner)
# g means group 
# o means others, YOU
```

#### ==** `sudo -i` vs `su`==
For some cases, root has no valid password, so instead of using `su`, use `sudo -i`. `su` asks you root password to get `#` root prompt, `su -i` asks you regular user password, if permitted by `sudoers` rules, you will be directed to root prompt.

#### ==** How to Check if you have Root Password Set==
```bash
sudo cat /etc/shadow | grep root
# any result with * (no valid password )or ! (account locked) means password is not available
```

#### ==** If Permission Denied==
**To modify a file**
```bash
echo "jal ALL=(ALL) ALL" | sudo tee /etc/sudoers.d/jal
```

**To change permission**
```bash
sudo chmod 440 /etc/sudoers.d/jal
```

#### ==** `sudo` flags==
```bash
sudo -i # login as root, get full root login shell
sudo -l # list, show effective active sudo privileges
sudo -k # kill, invalidate timestamp cache for password prompt
sudo -s # root shell, but still keep original user environment
sudo -v # validate, refresh cached sudo password
sudo -V # print sudo program version information
sudo -u <username> # run as another user
	sudo -u jal ls /home/jal
sudo -H # set HOME environment to root's home

```

#### ** What is an Environment and a Shell
Any running program in Linux is one country.

==Environment== is a handbook which holds key-value notes like commands, folder location, and user, it defines how a program should behave.

==Shell== is a special type of country, it also acts as reception secretary
Terminal != Shell, terminal is just the GUI window, while Shell is the like brain of the terminal.

`sudo -i` throw away old system and change into new system.
`sudo -s` keep handbook but change the ruler into root


#### ==** What `ls` command is==
It is a command where it create short-lived program, read your directory and return the read result to the user.

```bash
ls # normal ls
ls -l # long format
ls -a # show hidden files
ls -l /etc # list content of /etc folder
```

#### ==** What `/etc` folder is==
It is one of the most important system directory where it stores all config files for OS.

#### ** Other Interesting Commands
```bash
whoami # who are me
```


## * Switching between GUI and CLI
#### ==** Desktop, Workstation, and Server==
**Desktop** targeted for laptop user, what's installed is GUI, simple daily-use apps, and light developer tools
**Workstation** targeted for developers, engineers, what's installed is  GUI and heavy-duty developer tools.
**Server**, no GUI, what's installed is network-related services

#### ==** Virtual Terminals== 
**Graphical Terminal window vs Virtual Terminal**
Graphical terminal window is like the one inside GUI desktop, while virtual terminal takes your whole screen completely, GUI disappears entirely.

One VT is reserved for graphical desktop, the other are enabled for text logins.

It can be useful to troubleshoot problematic VT.

#### ==** Change between Virtual Terminals==
Press `CTRL - ALT - function key`

#### ==** Turning Off Graphical Desktop==
```bash
sudo systemctl stop gdm #or 
sudo telinit 3

sudo systemctl start gdm #or 
sudo telinit 5

# then restart it
```

`gdm` is GNOME Display Manager, it is a program (service) starts by the desktop, so it can be stopped.