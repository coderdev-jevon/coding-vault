### Questions

**Languages and tools (most relevant to you)**

1. Compiler vs interpreter: how does each run your code? Where does Python fall, and why does that matter when you compare it with C++ for performance? 🎯
2. What is a runtime? Why isn’t every language just converted to machine code?  🎯
3. Name a compiler for C/C++ and a debugger for C/C++. What does a breakpoint let you do? 🎯
4. What does version control do? Name two systems, and which one is the standard today?
5. A container is like a private room inside a house. What does that mean technically, and why are containers central to deploying AI models? 🎯
6. What is an IDE, and how is it different from a plain text editor like vim? 🎯
7. Name two terminal editors and two editors that are mainly graphical.

**Package checks (practical)**  
8. How can you tell whether an app was installed with `apt` or `snap`? Give one terminal method.  
9. What is the difference between `snap refresh APP` and `sudo apt upgrade`? Which command removes each kind?

**Protocols**  
10. IMAP, POP3, SMTP: which sends, which receives, and which keeps mail on the server?  
11. SFTP vs FTPS: what is one difference?

**Bonus (VM, 1 minute):** run `gcc --version`, `git --version`, and `snap list`. Which questions do they relate to?

### Answer key

1. A compiler translates all the source code into an executable binary first, then you run that. An interpreter reads, translates, and runs the code line by line. Python is interpreted, so it’s convenient but slower, which is why performance-critical AI code (like the inside of PyTorch) is written in C/C++ or CUDA and only called from Python.
2. A runtime is a bundle of libraries, tools, and services that executes your program. Some languages compile to an intermediate format that only the runtime understands (Java’s bytecode is the classic case), which makes the same program portable across systems.
3. GCC or Clang for compiling. GDB (or Valgrind for memory problems) for debugging. A breakpoint pauses the program at a chosen line so you can inspect its state.
4. It tracks every change to your files, so you can see history and go back. Git and SVN. Git is the standard.
5. A container is a group of processes isolated from the rest of the host, with its own filesystem and network settings, sharing the host’s Linux kernel. This is the namespaces idea you studied earlier. Models and their exact library versions are packaged in a container so they run identically everywhere, such as on cloud GPU machines.
6. An IDE bundles an editor, compiler or interpreter, debugger, and file manager in one program. A plain editor only edits text and you add the other tools yourself.
7. Terminal: vim, emacs. Graphical: VS Code, VSCodium.
8. `snap list APP_NAME`. If it appears, it’s a snap. In GNOME Software, the label says Snap. Everything in Synaptic is APT.
9. `snap refresh` updates a snap app. `sudo apt upgrade` installs newer versions of your apt packages (after `apt update` refreshes the catalog). Remove with `snap remove APP` or `sudo apt remove APP`.
10. SMTP sends. IMAP and POP3 receive. IMAP keeps mail on the server and syncs across devices, while POP3 downloads it to one computer.
11. SFTP runs over SSH. FTPS is the older FTP protocol secured with TLS (encryption).

**Bonus:** `gcc --version` relates to question 3, `git --version` to question 4, and `snap list` to questions 8 and 9. If gcc or git isn’t installed, that’s a useful discovery too.****