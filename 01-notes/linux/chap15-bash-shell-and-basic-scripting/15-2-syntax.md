# Chapter 15.2: Syntax
Date: 2026-10-19

---
## ==🔵* Basic Syntax and Special Characters==
---
![[shell-scripts-basic-syntax.png|444]]

---
## ==🔵* Splitting Long Commands Over Multiple Lines==
---
```bash
line1 \
line2 \
line3 \
```

---
## ==🔵* Putting Multiple Commands on a Single Line==
---
Also called as chaining of commands.

#### ==`;` (semicolon)== 
All of the commands will run
```bash
command1 ; command2 ; command3
```

#### ==`&&` (double ampersand)==
Commands will stop if previous command fails.
```bash
command1 && command2 && command3
```

#### ==`||` (double pipe)==
Commands will stop until one succeed
```bash
command1 || command2 || command3
```

---
## ==🔵* Output Redirection==
---
It is the process of diverting output to a file.

```bash
output > file # overwrite
output >> file # append
```

---
## ==🔵* Input Redirection==
---
It is the process of reading input from a file.

```bash
command < file
```
---