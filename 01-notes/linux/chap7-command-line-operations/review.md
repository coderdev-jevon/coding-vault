### Questions

**Remote work and logs**

1. What does SSH do, and how can you authenticate with it? Write the command to log in as `student` on `remote-server.com`. Why does this matter for AI work? 🎯
2. What are file streams 0, 1, and 2? What do `>`, `2>`, `2>&1`, and `|` do? 🎯
3. Write one command that runs `python train.py` and saves both normal output and errors into `run.log`. Then write the command to watch that file live. 🎯

**Finding things and disk space**  
4. `df` vs `du`: which tells you which partition is full, and which tells you which folder is using the space? Write one command for each, in human-readable sizes.  
5. `locate` vs `find`: what’s the difference in speed and freshness? What command refreshes `locate`’s database?  
6. Write a `find` command for regular files ending in `.log` under `/var/log` modified in the last 2 days.  🎯
7. What do `*`, `?`, and `[!set]` match? Why is `apt-get install "vmware*"` safer than the unquoted version?

**Permissions and sudo**  
8. Decode `-rw-r--r--`: file type, owner, group, and others. What is it in numbers? What does `chmod 440` give?  
9. What does the sudoers rule `student ALL=(ALL) ALL` mean, part by part? If two files in `/etc/sudoers.d/` give conflicting rules for the same user, which one wins?  
10. `sudo -i` vs `sudo -s`: what’s the difference?

**Paths and links**  
11. What do `.`, `..`, `~`, and `cd -` mean? What makes a path absolute vs relative?   🎯
12. Hard link vs symbolic link: if you delete the original file, what happens to each? 🎯

**Packages**  
13. `dpkg` vs `apt`: which is low-level and which is high-level? What’s the difference between `remove` and `purge`, and between `update` and `upgrade`?

**Bonus (VM, 1 minute):** run `df -hT -x tmpfs` and `ls -l /etc/sudoers.d`. Which questions do they relate to?

### Answer key

1. SSH runs a shell on another computer over the network. Authenticate with a password or an SSH key. `ssh student@remote-server.com`. Training machines and cloud GPUs are remote, so SSH is how you work on them.
	```bash
	sudo systemctl start ssh
	sudo systemctl enable ssh
	sudo jal@localhost
	```
2. 0 is `stdin` (input), 1 is `stdout` (normal output), 2 is `stderr` (errors). `>` sends output to a file, `2>` sends errors to a file, `2>&1` sends errors to the same place as output, and `|` feeds one command’s output into the next command’s input.
3. `python train.py > run.log 2>&1`, then `tail -f run.log`.
4. `df` shows free and used space per mounted partition: `df -h`. `du` shows how much space folders use: `du -sh *` or `du -h -d1 /home/jal`. Checkpoints and datasets fill disks fast, so you’ll use both.

5. `locate` searches a pre-built database, so it’s fast but can be out of date. `find` scans the disk live, so it’s slower but always current. Refresh with `sudo updatedb`.
6. `find /var/log -type f -name "*.log" -mtime -2`
7. `*` matches any string, `?` matches one character, and `[!set]` matches any character not in the set. Quotes stop the shell from expanding `vmware*` against files in your current folder, so `apt` receives the pattern itself and matches package names.
8. `-` regular file, `rw-` owner, `r--` group, `r--` others. That’s 644. `chmod 440` gives owner and group read-only and others nothing, which is what sudoers files require.
9. The first `ALL` is which hosts, `(ALL)` is which users it can run commands as, and the last `ALL` is which commands. Files are read in alphabetical order and the last matching rule wins, so `student` beats `nopasswd`.
10. `sudo -i` gives a full root login shell with root’s environment. `sudo -s` gives a root shell but keeps your current environment.
11. `.` is the current folder, `..` is the parent, `~` is your home, and `cd -` goes back to the previous directory. An absolute path starts with `/` and follows the tree from the root. A relative path starts from where you are.
12. Hard link: both names share one inode, so deleting the original leaves the other name working. Symlink: it’s a shortcut to the name, so deleting the original leaves a broken (dangling) link.
13. `dpkg` is low-level (unpacks packages, runs scripts) and `apt` is high-level (downloads from repositories and resolves dependencies). `remove` keeps config files and `purge` deletes them too. `update` refreshes the catalog and `upgrade` installs newer versions.

**Bonus:** `df -hT -x tmpfs` relates to question 4, and `ls -l /etc/sudoers.d` to questions 8 and 9. Check the permissions on any file there. It should be `-r--r-----` (440).