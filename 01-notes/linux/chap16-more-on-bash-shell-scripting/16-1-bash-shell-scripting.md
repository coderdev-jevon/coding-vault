# Chapter 16.1: String Manipulation
Date: 2026-10-25

---
## ==🔵* String Manipulation==
---
```bash
[[ string1 > string2 ]] # compare sorting order
[[ string1 == string2 ]] # compare characters
myLen=${#string1} # save the length of string1
```

#### ==Elements Breakdown==
```bash
[] # regular command
[[]] # bash keyword
[[ x ]] # space around brackets -> recognization of first and last argument
${} # parameter expansion
```

```bash
[ $a = "x" ] # not okay
[ "$a" = "x" ] # okay
[[ $a = "x" ]] # okay

[[ $a = $b ]] 
[[ $a == $b ]] # both are identical

[ "$a" = "$b" ] # works in every shell
[ "$a" == "$b" ] # works in bash only
```
---
## ==🔵* String Indexing==
---
```bash
${string:0:n} # string:start:number of characters
${string#*.} # remove characters before .
# '#' remove shortest matching prefix
# * any character
# . dot
```
---
## ==🔵* The `case` Statement==
---
```bash
case expression in
	pattern1) execute commands;;
	pattern2) execute commands;;
	pattern3 | pattern4) execute commands;; # | means or
	* ) execute some default commands;;
esac
```
---
## ==🔵* The `for` Loop==
---
```bash
for variable_name in list
do
	task
done

```
---
## ==🔵* The `while` Loop==
---
```bash
while condition
do
	task
done
```
---
## ==🔵* The `until` Loop==
---
Essentially opposite of while loop
```bash
until condition
do
	task
done
```
---
## ==🔵* Script Debugging==
---
#### Run Bash Script on Debug Mode
```bash
bash -x ./script_file

# or

set -x # turn on
scripts
set +x # turn off
```
---
## ==🔵* Redirecting Errors to File and Screen==
---
`stdin` - 0
`stdout` - 1
`stderr` - 2

```bash
cat file 2> error.log # save the error message
```
---
## ==🔵* Create Temporary Files and Directories==
---
Why not create own temporary file? Predictable file can be easy for hackers to gain access. It can lead to damage of overwritten important data with temporary data.

#### ==`mktemp`==
```bash
TEMP=$(mktemp /tmp/tempfile.XXXXXX) # X minimum 3 characters
TEMPDIR=$(mktemp -d /tmp/tempdir.XXXXX)
```
---
## ==🔵* Discarding Output with `/dev/null`==
---
`/dev/null` also called as black hole, it discard everything

```bash
ls -lR /tmp > /dev/null # only output discarded
ls -lR /tmp >& /dev/null # both output and error discarded
	ls -lR /tmp > /dev/null 2>&1 # send 2 to where 1 is
```

---
## ==🔵* Random Numbers and Data==
---
```bash
$RANDOM
```

#### ==How to Kernel Generates Random Number==
It is not based on pure logic

Collect noise (keystrokes, hardware sources, and others) ->Entropy pool -> `/dev/urandom` (more modern) or `/dev/random`

---
