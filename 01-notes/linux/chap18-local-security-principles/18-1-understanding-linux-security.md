# Chap 18.1: Understanding Linux Security
Date: 2026-10-27

---
## ==🔵Vocabulary==
---
1. Authentication - who are you
2. Authorization - what may you do
3. Command logging - system records on which commands were run
4. Hard disk - a part of computer that stores your data permanently
5. Device nodes - doorway to the real hardware
6. Proprietary software - software owned by company or person who controls how it can be used (source code kept secret)



---
## ==🔵User Accounts==
---

User accounts can be modified by `useradd` and `userdel`
|
Users are identified by their user id.
|
User id can be viewed in `/etc/passwd`
|
Only authenticated users are able to access files and applications.

---
## ==🔵Types of Accounts==
---
The purpose of distinguishing account types is for isolating processes (whether the work of one user affect the other users or not)

1. `root`
2. `System`
3. `Normal`
4. `Network`

#### ==`last` utility==
`last` show last time each user logged in to the system, it might potentially show inactive accounts.

---
## ==🔵Understanding the `root` Account==
---
It has no security restrictions.

`#` at shell prompt shows that you have the absolute power.

---
## ==🔵Operations Requiring `root` Privileges==
---
1. Creating, removing, and managing user accounts
2. Managing software packages
3. Removing or modifying system files
4. Restarting system services
---
## ==🔵Operations Not Requiring `root` Privileges==
---
1. Running network client
2. Using devices like printers
3. Run operations that the user has proper permissions to access
4. Running SUID-root applications

SUID (Set owner User ID upon execution), allows ordinary users to do one specific task that normally needs higher privileges.

---
## ==🔵Comparing `sudo` and `su`==
---
`sudo`:
1. Asked to enter passwords after each commands or after configurable time interval
2. Has detailed logging features (logs tracking)
3. Controlled and limited

`su`:
1. User can logged in how long they want to
2. Limited logging features
---
## ==🔵`sudo` Features==
---
User's authorization for using `sudo` is based on configuration information in `/etc/sudoers` and `/etc/sudoers.d`

You can look at attempt on root access at `/var/log`

---
## ==🔵The `sudoers` File==
---
#### ==Structure of Entries== 
```bash
who where = (as whom) what 

# where - on which machine
# as whome - costume to wear. default is root, you can choose any user by -u 
# what - what commands
```

For individual user -> edit file inside `/etc/sudoers.d` not the main `/etc/sudoers`

#### ==How to Edit `sudoers` File==
Use `visudo` to ensure
1. Only one user is editing the file
2. The user has proper permission
3. Refuse to write out the file if there are syntax errors

```bash
visudo /etc/sudoers # main file
visudo -f /etc/sudoers.d/jal # individual user
```

---
## ==🔵Command Logging==
---
Stored inside `/var/log/auth.log`

![[sudo-command-logging-example.png]]

#### ==5 Elements of Command Logs==
1. Calling username - `jal`
2. Terminal info - `TTY=pts/0` (Teletypewriting=pseudo-terminal salve - number of the terminal)
3. Working directory - `PWD=/etc/sudoers.d`
4. User account invoked - `USER=root`
5. Command with arguments - `COMMAND=/usr/bin/whoami`
---
## ==🔵Process Isolation==
---
Linux is more secure than other operating systems because Linux maintain each process having their own private space.
|
Linux make it difficult for viruses to attack resources on the system.

#### ==More Security Mechanisms==
1. Control Groups (`cgroups`)
	It allows group administrators to group processes and limit system's resources to each group.
2. Containers
	Run multiple isolated Linux systems on a single system
3. Virtualization
	Each computer can run several complete computers (virtual machine) inside it
---
## ==🔵Hardware Device Access==
---
Hard disks device nodes are represented as `/dev/sd*`

---
## ==🔵Keeping Current==
---
Once someone find security flaw in software (Linux kernel, applications, libraries), fixes are released.
|
Keep your system updated (Linux mechanism for automatic updates)

---
## ==🔵How to Change Users==
---
```bash
sudo su newuser # you -> root -> newuser

ssh newuser@localhost # connects to local SSh server
```
---
## ==🔵Working with Passwords==
---
#### ==Where Passwords is Stored?==
In older system, encrypted password is stored in `/etc/passwd` and can be viewed by everyone.

In modern system, encrypted password is stored in `/etc/shadow` and can only be viewed by root.

#### ==Password Encryption==
The most tested hashing algorithm is SHA-512 (Secure Hash Algorithm). 
```bash
echo -n test | sha512sum # -n means no new line, sha512 receive file input, sum means checksum
```
#### ==Good Password Practices==
1. Password aging - create new password after a specific period
	```bash
	chage -l # stands for change age, show aging information
	```
2. Force users to set strong passwords using Pluggable Authentication Modules (PAM)
3. Install password cracking programs, such as John The Ripper, to identify weak passwords

---
## ==🔵Securing the Boot Process and Hardware Resources==
---
#### ==Requiring Boot Loader Passwords==
Boot loader password stop a user changing how the system boots, by locking GRUB menu. It was quite complicated to edit password in GRUB version 2, but the features are more vary

```bash
# Edit in
/etc/grub.d/
/etc/default/grub

# Then
update-grub
```



However, it does not stop user booting from alternative media. So, user must used BIOS password for full protection.

`Power on -> BIOS/UEFI -> Boot loader (GRUB) -> Kernel -> Login`

#### ==Hardware Vulnerability==
Potential attack:
1. Key logging - real-time activity of computer user
2. Network sniffing - capturing and viewing the network packet movement
3. Boot a live USB
4. Remounting and modifying disk content

Defending protocols:
1. Lock down work stations and servers
2. Protect network links
3. Protect keyboards from tampering
4. Add BIOS password

#### ==Software Vulnerability==
Linux is fast in exposing and fixing vulnerabilities.

---