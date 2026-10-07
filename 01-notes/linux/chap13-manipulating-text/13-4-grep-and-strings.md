# Chap 13.4: Grep and Strings
Date: 2026-10-16

## ==* `grep`==
Scan files for specified patterns
```bash
grep [pattern] <filename>
grep -v [pattern] <filename> # v stands for invert, so excluding pattern
grep [0-9] <filename>
grep -C 3 [pattern] <filename> # c for context, 3 lines before and after the match
```

## ==* `strings`==
Used to extract all printable character strings

```bash
strings -f [h-k]* | grep GPL # run strings on all the files starting with h,i,j,k then filters output so only lines containing GPL are shown
```

