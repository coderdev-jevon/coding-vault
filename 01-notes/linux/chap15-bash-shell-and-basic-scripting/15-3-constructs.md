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
	statements
else
	statements
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
