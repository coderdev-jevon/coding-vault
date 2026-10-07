## Chap 13.1: `cat` and `echo`
Date: 2026-10-06

## * Command Line Tools for Manipulating Text Files
NOTHING

## * `cat`
`cat` is short for concatenate
#### ==** `cat` to view file==
```bash
cat filename # to look at file content
tac filename # print lines of a file in reverse order
```

#### ==** `cat` to concatenate==
```bash
cat file1 file2 # concatenate file1 with file2
cat file1 file2 > newfile # output into new file
cat file >> existingfile # append file to end of existing file
cat > file # overwrites and write new text until CTRL-D
cat >> file # append to file until CTRL-D

cat > file << EOF # stop until write EOF
cat > file << STOP # stop until write STOP
```

## * `echo`
```bash
echo string > newfile
echo string >> existingfile
echo $variable
```

#### ** `echo` with option
```bash
echo -e "Hi \nBye" # -e eanble \n and \t, e stands for escape
```

## * Working with Large and Compressed Files
==use `less` to make large files to be more readable==
```bash
less somefile
cat somefile | less
```

## * `head`
```bash
head -n 5 filename # read first 5 lines
head -5 filename # read also the first 5 lines
```

## ==* `tail`==
```bash
tail -n 15 filename
tail -15 filename
tail -f filename # f stands for follow, to monitor new output in growing log file
```

## * Viewing Compressed Files
Utilities with z prefixes are usually for compressed files.
==`zcat, zless, zdiff, zgrep`==
```bash
zcat compressed-file.txt.gz
zless somefile.gz # newer version
zmore somefile.gz # older version
zgrep -i less somefile.gz # look at "less" case-insensitive inside file somefile.gz
zdiff file1.txt.gz file2.txt.gz # find the difference between two files
```

Other compression methods (`gzip, xz, bzip2`)
`xzcat, xzless, xzdiff...`

