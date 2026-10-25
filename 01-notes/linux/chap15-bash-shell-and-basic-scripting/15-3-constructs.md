# Chapter 15.3: Constructs
Date: 2026-10-22

---
## ==🔵* The `if` Statement==
---
```bash
#1
if condition; then statement; fi

#2
if condition
then
	statement
elif [condition1] || [condition2]
then
	statement
else
	statement
fi
```

---
## ==🔵* Implementation `if` Statement==
---
```bash
if [ -f "$1" ]
then
	echo file "$1" exists
else 
	echo file "$1" does nto exist
	fi
```
---
## ==🔵* Testing for Files==
---
```bash
if [-x /etc/passwd ] ; then # test executable or not
	statement
fi
```

![[testing-for-files-shell-scripts.png|503]]

#### ==Additional==
1. Numbers
```bash
if [ $number1 -gt $number1 ] # greater than

-eq # equal
-ne 
-lt 
-ge # greater than or equal to
-le
```
2. Strings
```bash
if [ string1 == string2 ]; then
	statement
fi
```

---
## ==🔵* Boolean Expressions==
---
`&&`, `||`, `!`

---
## * Arithmetic Expressions
---
```bash
expr 8 + 8 # old way
echo (expr 8 + 8) # old way
echo ((8 + 8))
let x=( 1 + 2 ); echo $x
```