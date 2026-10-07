# Chap 13.3: File Manipulation Utilities

## ==* `sort`==
```bash
sort <filename> # sort according to characters at beginning
cat file1 file2 | sort
sort -r <filename> # sort in reverse order
sort -k 3 <filename> # sort by 3rd field on each line, k stands for key
sort -u <filename> # u stands for unique, also checks for unique values
```

## * `uniq`
It ==removes duplicate consecutive lines==

==Run `sort` first==, then run `uniq`

```bash
uniq <filename>
uniq -c <filename> # count the number of duplicate entries
```

## * `paste`
```bash
-d # to specify delimiters
-s # to append data in series instead of parallel
```

#### ==** Using `paste`==
```bash
paste file1 file2
paste -d, file1 file2
```

## ==* `join`==
It joins two files based on their common fields
```bash
join file1 file2
```

## ==* `split==`====
Usually split into 1000-line segments
```bash
split infile
split infile <Prefix>
split -l n infile # each file has n lines each
```

#### ==** `wc`==
word count -> to count words
```bash
wc -l linux.words
```

## ==* Regular Expressions and Search Patterns==

![[regular-expressions.png|487]]

#### ** Use Regular Expressions and Search Patterns
```bash
a.. # a and two characters
b.|j.
..$ # two characters and end of the line
l.*
l.*y
the.*
^..# start of the line and two characters
```