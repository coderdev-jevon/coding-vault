
# Chap 18.1: Understanding Linux Security
Date: 2026-10-27

---
## Vocabulary
---
1. Authentication - who are you
2. Authorization - what may you do


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
## ==🔵Safe Working Environment Protocol==
---
1. Remove inactive accounts 