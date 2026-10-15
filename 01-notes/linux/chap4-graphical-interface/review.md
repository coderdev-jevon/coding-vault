### Questions

**Core concepts (most important for your goal)**

1. In Windows the desktop is built into the OS. How is it different in Linux, and why does that matter for servers? 🎯
2. What are the three core components of a desktop environment? 🎯
3. Name the two window systems on Ubuntu. Which is the modern one? 🎯
4. Linux allows multiple users on one system. How do you switch users on the desktop?

**Files and hidden items (reused constantly in terminal work)**  
5. What does a leading `.` in a file name mean, and what are such files usually for? What shortcut shows them in the file manager?  🎯
6. What command creates an empty file from the terminal? What is the default GNOME text editor?  🎯
7. Where is the Trash folder, and what is the path? (Hint: it’s a hidden location.) 🎯

**Session management**  
8. Why should you shut down properly instead of just cutting power? What could happen to your data?  🎯
9. What is the difference between locking the screen, suspending, and shutting down? What happens to running apps in each?

**Quick recall**  
10. Match the shortcut to its action: `Ctrl+L`, `Ctrl+F`, `Ctrl+H`, `Super+L`. 🎯

**Bonus (VM, 1 minute):** run `ls -a ~` and `echo $XDG_SESSION_TYPE`. Which questions do the results relate to?

### Answer key

1. In Linux the desktop is separate software, called a desktop environment, that you install on top of the core OS. Because it’s optional, servers can run with no GUI at all, only a command line. That’s how most AI and cloud machines work.
2. The session manager (starts and maintains the graphical session), the window manager (how windows are displayed), and a set of utilities and applications.
3. Wayland (modern) and X11/Xorg (older).
4. Use the switch user option from the login screen.
5. A leading `.` makes a file hidden. These are usually configuration files. `Ctrl+H` shows them in the file manager, and `ls -a` shows them in the terminal.
6. `touch filename`. The default editor is `gedit`.
7. `~/.local/share/Trash/files`. Right-click Trash in the left panel and choose Empty Trash to delete everything in it.
8. A proper shutdown saves unsaved data and prevents filesystem corruption. Cutting power can lose data and damage the filesystem, which matters for long jobs like model training.
9. **Lock:** the screen is protected, but apps keep running. **Suspend:** like sleep in Windows, with activity paused and everything kept in place. **Shutdown:** apps are closed and the system powers off, so save your work first.
10. `Ctrl+L` goes to a typed directory path, `Ctrl+F` searches for files, `Ctrl+H` shows hidden files, and `Super+L` locks the screen.

**Bonus:** `ls -a ~` shows hidden files in your home folder (question 5). `echo $XDG_SESSION_TYPE` prints `wayland` or `x11`, which answers question 3 for your own VM.