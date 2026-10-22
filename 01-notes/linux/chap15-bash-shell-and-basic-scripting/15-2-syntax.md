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
## ==🔵* Built-In Shell Commands==
---
Built-In Shell Commands can be:
1. Compiled applications (`/usr/bin` one of them)
	translated into machine code ahead, like `ls, rm, df, gzip`, not bash code
2. Built-in bash commands
	two separate reasons: must be built-in because it changes the shell itself, like `cd` or  built-in for speed
3. Other scripts from other languages
	`#!/usr/bin/python3, #!/usr/bin/perl`
---
## ==🔵* Commands Built-In to `bash`==
---
lists can be view from `help` command

---
## ==🔵* Script Parameters==
---
```bash
./script.sh /tmp
$0 # script name
$1 # first parameter
$2 # second parameter
$* # all paramters
$# # number of arguments
```
---
## ==🔵* Command Substitution==
---
Output of inner command -> Portion of another command

`$()` or backticks, `$()` is more modern and preferrable for command nesting

```bash
ls /lib/modules/$(uname -r)
```
---
## ==🔵* Environment Variables==
---
can be seen through `env, set, printenv`

make your own by `VARIABLE_NAME=VALUE`

---
## ==🔵* Exporting Variables==
---
Look at list of exported variables by `export`, child processes only get copies to values.

#### ==Export Variables==

```
export VAR=value

VAR=value ; export VAR
```
---
## ==🔵* Functions==
---
Useful for executing procedures multiple times

Declaring -> Calling

#### Write Function Syntax
```bash
function_name () {
	command...
}
```
---
## ==🔵* `if` Statement in Shell Scripts==
---
```bash
[[ -d $NEW_DIR ]] && echo "%NEW_DIR already exists, aborting" && exit

# after && execute when inside [[]] is true


if [[ condition ]]; then
	commands
elif [[ other_condition ]]; then
	commands
else 
	commands
	
	
if (( condition )) # also valid
```
---
## ==🔵* `for` loop Syntax in Bash==
---
```bash
for variable in item1 item2 item3;
do
	commands $variable
done
```

---
## ==🔵* Fun Facts==
---
#### ==`uname`==
this command prints basic info about system you are running on
```bash
uname -r # prints kernel release
```
---