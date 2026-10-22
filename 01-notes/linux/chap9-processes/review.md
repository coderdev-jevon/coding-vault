### Questions

**Processes**

1. Program vs process vs thread: how does each relate to the others? What resources does a process need? 🎯
2. Name the process types. Which type is `sshd`, and which is Firefox? 🎯
3. What are a PID and a PPID? What is PID 1, and how does that link to the boot chapter? 🎯
4. Write the commands to find the PID of a process called `python`, stop it politely, then force-kill it. What signal does each send, and why try the polite one first? 🎯
5. What is the nice value range, and which direction means higher priority? What command changes a running process’s nice value? What can a regular user not do with it? 🎯

**Reading the system**  
6. Read `load average: 4.00 2.50 1.00` on a 4-CPU machine. Is it busy? Is it getting better or worse? Which command shows the CPU count?  
7. In `top`, what do `us`, `sy`, `id`, `wa`, and `st` mean? If a training job is slow and `wa` is high, what does that suggest? What does it mean when swap use grows?   🎯
8. `ps aux` vs `ps -ef`: which style is which? How do you see the parent-child tree?

**Background jobs**  
9. How do you run a command in the background from the start? A job is already running in the foreground: which keys and commands move it to the background and back? How do you list jobs?  🎯
10. What happens to a background job when you close the terminal? Write the command that avoids that. 🎯

**Scheduling**  
11. `at` vs `cron` vs `anacron`: what is each for? Write the cron line that runs `/home/student/backup.sh` every day at 02:00, and name the five time fields in order. 🎯

**Scenario**  
12. You SSH into a GPU server, run `python train.py`, and your laptop sleeps. The job dies. Why? Give one fix from your notes, and name the commands to check later that it’s still alive and how busy the machine is.

**Bonus (VM, 1 minute):** run `uptime`, `nproc`, `sleep 100 &`, then `jobs` and `ps aux | head`. Try `echo start; sleep 5; echo end` too. Which questions do they relate to?

### Answer key

1. A program is the blueprint, a process is a running instance of it, and threads are workers inside one process that share its memory. A process needs memory, CPU time, and peripherals such as disk.
2. Interactive (started by a user, like Firefox), batch (queued, via `at` or `batch`), daemon (a background server, like `sshd` or `httpd`), threads, and kernel threads (like `kthreadd`). `sshd` is a daemon and Firefox is interactive.
3. The PID is the process’s ID, and the PPID is the ID of the process that started it. PID 1 is `init`, which is `systemd`, started by the kernel at the end of boot and the parent of all processes.
4. `ps aux | grep python`, `ps` stands for process status, finds the PID, then `kill <pid>` (SIGTERM, a polite request to exit) and `kill -9 <pid>` (SIGKILL, forced). Try the polite one first so the program can save state and clean up. A forced kill gives it no chance.
5. Range is -20 to +19, and a lower value means higher priority. `renice +5 <pid>` changes it. A regular user can only make a process nicer (raise the value) and can’t raise its priority. That needs root.
6. The 1-minute figure (4.00) means about 4 tasks wanting CPU, which fully uses 4 CPUs. The 5- and 15-minute figures are lower, so the load is rising. `nproc` gives the CPU count. Compare load to CPU count, since load below the CPU count means headroom.

	run it by `top`

7. `us` is user programs, `sy` is kernel, `id` is idle, `wa` is waiting on disk or other I/O, and `st` is time stolen by other VMs. High `wa` suggests the job is waiting on disk, such as slow data loading, rather than lacking compute. Growing swap use means RAM is exhausted, and swap is a much slower disk, which hurts training badly.
8. `ps aux` is BSD style (no dash) and `ps -ef` is System V style. `pstree` shows the tree, as does `ps lf`.
9. `command &` starts it in the background. For a running job: `Ctrl+Z` suspends it, `bg` resumes it in the background, and `fg` brings it back to the foreground. `jobs` (or `jobs -l`) lists them.
10. It is killed with the terminal. Use `nohup command &` so it keeps running. -> it stands for no hang up
11. `at` runs a job once at a given time. `cron` runs recurring jobs from crontab. `anacron` runs jobs that were missed because the machine was off. The line is `0 2 * * * /home/student/backup.sh`, with fields minute, hour, day of month, month, day of week.
12. The SSH session closed, so the terminal’s jobs were killed with it. Fix: `nohup python train.py &` (a terminal multiplexer like `tmux` is also very common for this, though it’s not in your notes). To check later, reconnect and use `ps aux | grep train` for the process, and `uptime` or `top` for load.