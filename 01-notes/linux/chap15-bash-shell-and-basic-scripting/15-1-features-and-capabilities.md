# Chapter 15.1: Features and Capabilities
Date: 2026-10-18

---
## ==🔵* Shell Scripting==
---
Shell scripting purpose is to automate set of commands.

---
## ==🔵* Shell Scripts==
---
Shell is a command line interpreter (interprets and executes your code line by line).

#### ==** Comparison Command Line vs Script File==
```bash
# COMMAND LINE
find . -name "*.c" -ls 
```

```bash
# SCRIPT FILE
#!/bin/bash -> full path command line interpreter
find . -name "*.c" -ls
```

---
## ==🔵* Simple bash Script==
---
```bash
cat > hello.sh

bash hello.sh # run script file
./hello.sh # but, you need to change access for x
```
---
## ==🔵* Interactive Example Using `bash` Scripts==
---
```bash
#!/bin/bash
echo "ENTER YOUR NAME"
read name # pause script, wait user to type, store in variable
echo "The name given was $name"
```
---
## ==🔵* Return Values==
---
Every time script finishes, it returns a number. 
Set it with `exit` command, and read it by `$?`

0 -> Success
1 -> General Error, no match, fail intentionally
2 -> Serious Error, bad usage, inaccessible



---
---
## ==🔵* Review Previous Lessons==
---
#### ==** `"*.c"`==
`*.c` is a glob pattern, * means any number of characters including none, so this glob pattern means any filename whose name ends in `.c`. 

#### ==** `-ls` option on `find` command==
```bash
find . -ls # . means start at current directory, means print in detailed
```

#### ==** `chmod` syntax==
```bash
chmod +x script.sh          # add execute for everyone
chmod u+x script.sh         # add execute for owner only
chmod go-w file.txt         # remove write from group and others
chmod a+r file.txt          # everyone can read
chmod u=rwx,g=rx,o= file    # set exact permissions (others get none)
```
---