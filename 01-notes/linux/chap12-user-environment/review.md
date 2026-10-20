### Questions

**Users and groups (12.1)**

1. `whoami` vs `who` vs `id`: what does each report? 🎯
2. Which two files store users and groups? Write the command to create user `trader` with a home directory, a full-name comment, and `/bin/bash`, then set the password and check it. What do `userdel trader` and `userdel -r trader` each leave or remove? 🎯
3. Write the command to add an existing user to the group `docker` without removing their other groups. What goes wrong if you forget `-a`? How do you remove a user from a group, and when does a group change take effect? 🎯
4. `su` vs `sudo`: which is preferred, and why? Where is sudo’s configuration stored? 🎯

**Environment variables (12.2)**  
5. Local variable vs environment variable: what does `export` change? Why would `python train.py` not see a variable you set without `export`? How do you set a variable for one command only (for example, to choose GPU 0)?  🎯
6. Where do you make a variable permanent? How do you apply it without logging out? Why doesn’t a variable you set in one terminal appear in another terminal?   🎯
7. What is `PATH`, and in what order is it searched? Write the command to append `/home/you/tools/bin`. What did your fake `ls` experiment show about append vs prepend, and what is the danger of prepending or of an empty entry?  🎯
8. Write a command that creates an alias `ll` for `ls -lah`. How do you list aliases, remove one, and make one survive a new terminal?  🎯
9. What do `$HOME`, `~`, `$SHELL`, and `$PS1` hold? What do `\u`, `\h`, `\w` mean, and why save `OLD_PS1` before changing the prompt?

**History (12.3)**  
10. What do `!!`, `!$`, `!n`, `!string`, and `Ctrl+R` do? Where is history stored, and what’s the difference between `HISTSIZE` and `HISTFILESIZE`?  🎯
11. Scenario: you typed `export API_KEY=abc123` in the terminal. Where does that now live? Name two ways to avoid or fix it.🎯

**Ownership and permissions (12.4)**  
12. Decode `-rwxr-xr--` into letters per group and numbers. What do 755, 600, and 440 mean, and when would you use each? What does `chmod uo+x,g-w file` do?  🎯
13. `chown` vs `chgrp` vs `chmod`: one line each. Scenario: you created a folder with `sudo` and now can’t edit its files. Write the fix. 🎯
14. Scenario: SSH refuses your private key, saying its permissions are too open. What do you run? 🎯

**Bonus (VM, 1 minute):** run `id`, `ls -l /etc/passwd /etc/shadow`, `echo $PATH | tr ':' '\n'`, and `history | tail -5`. Which questions do they relate to?

### Answer key

1. `whoami` prints your current username. `who` lists users currently logged in. `id` shows UID, GID, and groups for you, or for a named user (`id user_name`).
2. `/etc/passwd` is the user database and `/etc/group` lists groups and members. `sudo useradd -m -c "Pro Trader" -s /bin/bash trader`, then `sudo passwd trader` (it prompts you to type the password), then `id trader` or `grep trader /etc/passwd`. `userdel trader` removes the account but keeps `/home/trader`, and `userdel -r trader` removes the home directory too.
3. `sudo usermod -a -G docker user_name`. Without `-a`, the user’s groups are replaced with only `docker`, which can strip them from groups like `sudo`. Remove with `sudo gpasswd -d user_name group`. The change applies at the user’s next login. Check with `groups user_name`.
4. `su` starts a shell as another user and needs that user’s password, while `sudo` runs single commands with your own password, under rules you control. `sudo` is preferred because it’s more limited and logged. Config is in `/etc/sudoers` and `/etc/sudoers.d/`.
5. A local variable exists only in the current shell. `export` makes it an environment variable that child processes inherit. A script you launch is a child process, so without `export` it can’t see the variable. For a single command: `CUDA_VISIBLE_DEVICES=0 python train.py`.
6. Put `export VAR=value` in `~/.bashrc`. Apply with `source ~/.bashrc` (or `. ~/.bashrc`), or open a new shell. A variable lives in one shell process and its children, so a separate terminal is a different process with its own environment.
7. `PATH` is a colon-separated list of directories searched for commands, left to right. Append with `export PATH="$PATH:/home/you/tools/bin"`. Appending puts your folder last, so real commands win. Prepending puts it first, so your fake `ls` won. Prepending an untrusted folder is a risk, and an empty entry means “the current directory,” which is also risky. Keep `$PATH` in the new value or you’ll lose the existing entries.
8. `alias ll='ls -lah'`. List with `alias`, remove with `unalias ll`, and make it permanent by adding the line to `~/.bashrc`.
9. `$HOME` is your home directory (`~` is shorthand for it), `$SHELL` is your default shell program, and `$PS1` is the prompt string. `\u` is the user name, `\h` is the host name, and `\w` is the current directory. Saving `OLD_PS1=$PS1` lets you restore the prompt if an experiment breaks it.
10. `!!` repeats the last command (`sudo !!` reruns it with sudo), `!$` is the last argument of the previous line, `!n` runs command number `n` from `history`, `!string` runs the most recent command starting with that string, and `Ctrl+R` searches history backward. It’s stored in `~/.bash_history`, written when the shell exits. `HISTSIZE` is how many commands are kept in memory for the session, and `HISTFILESIZE` is how many lines the history file keeps.
11. It’s saved in plain text in `~/.bash_history`. Avoid it by setting `HISTCONTROL=ignorespace` and starting the command with a space, or by keeping the key in a `chmod 600` file and loading it from there instead of typing it. Fix it afterward with `history -d N` (delete line N) and by editing `~/.bash_history`. If the key was ever shared or logged anywhere else, rotate it.
12. `-` regular file, owner `rwx` (7), group `r-x` (5), others `r--` (4), so 754. 755 is owner full and everyone else read and execute (scripts, programs, folders). 600 is owner read/write only (private keys). 440 is read-only for owner and group (sudoers files). `chmod uo+x,g-w file` adds execute for user and others and removes write from the group. On a directory, `x` means you can enter it.
13. `chown` changes the owner (`owner:group` sets both), `chgrp` changes the group, and `chmod` changes the permission bits. Fix: `sudo chown -R jal:jal folder` (`-R` covers everything inside), then check with `ls -l`.
14. `chmod 600 ~/.ssh/id_rsa` (use your key’s file name). SSH requires that only you can read a private key.

**Bonus:** `id` relates to question 1. `ls -l /etc/passwd /etc/shadow` relates to questions 2 and 12 (notice that only root can read `shadow`, where passwords are stored). The `PATH` line relates to question 7, and `history | tail -5` to question 10.