# Chap 12.1: Accounts, Users, Groups
Date: 26-10-03

## * Identifying Current User
```bash
whoami # to identify current user
who # to identify currently logged-on users
	who -a # a stands for all, eight flags at once
```

## * User Startup Files
==`/etc` files are the global settings== for all users
==~ home== files can include or override the global ones

A ==startup file is just a list of commands==, you can do anything there.

## * Order of the Startup Files
NOT NEEDED

## ==* Creating Aliases==
Often, aliases are placed in `~/.bashrc` file

```bash
alias # list all aliases
unalias # remove an alias

alias l="ls -CF" # create alias by double quotes
alias l='ls -CF' # create alias by single quote
```

To make alias persistent, place it inside ==`~/.bashrc` file==
## * Basics of Users and Groups
Every users are assigned to ==unique user ID (`uid`).== 
Linux uses ==groups to organize users== (groups with certain shared permissions).

==`/etc/group`== shows list of groups and their members. Permissions edit can be done at group level.
==`/etc/passwd`== user database

Every user belongs to one or more groups, each with ==`gid`==, default GID has the same name and number as the user. 

## * Adding and Removing Users
	Only root user can add or remove users and groups
```bash
useradd # adding new user
	sudo useradd jevon # add user "jevon"
userdel # remove existing user
	userdel jevon # but leave with home directory
	userdel -r jevon # remove home directory as well
```

After adding new user `jevon`, by default, their ==home directory is set to `/home/jevon`== and adds ==a line to `/etc/passwd`==, and ==default shell to `/bin/bash`==

## * User Information
```bash
id # report information about current user
id user_name # report information about that user
```

## * Using User Account
Several useful options
```bash
-s # login shell of new acount
-m # create home directory
-c # comment, possible to specify full name

sudo useradd -m -c "Pro Trader" -s /bin/bash trader
sudo passwd # trader123
```

Login to another user by `ssh`, secure shell login
```bash
ssh trader@localhost
exit # to exit from account
```

The default of ==`/home/trader` can be seen from `/etc/skel`==

More, you can look at ==`/etc/default`== -> file ==grub== inside

```bash
grep penguin passwd group
```

## * ==Adding and Removing Groups==
```bash
sudo /usr/sbin/groupadd anewgroup # create new group
	sudo groupadd anewgroup # is also really possible
sudo /usr/sbin/groupdel anewgroup # delete a group

groups user_name # look what groups user are in
sudo /usr/sbin/usermod -a -G anewgroup user_name # add user to new group

sudo gpassword -d engineer sudo # gpassword stands for group password, -d is delete, sudo is the group to remove the user from
```

## ==* The Root Account==
Can be called as administrator account (other OS), or superuser in Linux.

You can use `sudo` commands to assign only limited access to commands.

## * `su` and `sudo`
==`su` stands for substitute user,== it launches new shell as another user (as a root for example).

==`sudo` is less dangerous== and preferred.

## * Elevating to Root Account
Configuration files to `sudo` is place in ==`/etc/sudoers`== file and ==`/etc/sudoers.d`== directory
