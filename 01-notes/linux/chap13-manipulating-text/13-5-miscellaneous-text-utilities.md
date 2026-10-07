Date: 2026-10-07

## ==* `tr`==
It is stands for translate and ==used to translate specified characters into another characters or delete them.==

```bash
tr [options] set1 [set2]
```
Sometimes use '' (single quote) to separate sets
#### ** How to use `tr`
```bash
cat filename | tr a-z A-Z
tr '{}' '()'

echo "This is for testing" | tr [:space:] '\t'
echo "This is for testing" | tr -s [:space:] # prevent space to appear in a row, s stands for squeeze

echo "You know whatz" | tr -d 'z' # d stands for delete

echo "My password is 12345" | tr -cd [:digit:] # c stands for complement, this remove everything except digits

tr -cd [:print:] < file.txt # command is always on the left, while file on the right
tr -s '\n' ' ' < file.txt
```

## ==* `tee`==
It stands for T-shaped pipe fitting, splits one flow of water into two directions.

It ==brings output to both standard output and file (saved to file)==

## ==* `wc`==
It stands for ==word count==, ==counts number of lines, words, and characters in a file or list of files==


```bash
-l # display number of lines
-c # display number of bytes
-w # display number of words
-m # display number of characters
```

## * `cut`
It is used to cut and extract specific columns, delimiters default is tab
```bash
cut -f2 filename # only extract the second column

cut -d" " -f3 filename # specify delimiters as space and extract the third column
```
