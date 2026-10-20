### Questions

**Viewing and redirecting**

1. `cat` vs `tac`: what’s the difference? What do `>` and `>>` do? Write a heredoc (`<< EOF`) that creates `config.yaml` containing two lines. How do you end input in `cat > file`? 🎯
2. You have a huge `data.csv` and a compressed `train.log.gz`. Write commands to: see the first 5 lines, count the lines, and search the compressed log for “error” ignoring case without extracting it.🎯
3. What do `grep -v`, `grep -C 3`, and `grep -c` do? Write one command that shows 3 lines of context around “CUDA out of memory” in `train.log`, and one that hides comment lines and blank lines from a config file. 🎯

**Editing and extracting text**  
4. What do `sed 's/cat/dog/'` and `sed 's/cat/dog/g'` each do? Does either change the file? What does `-i` add, and how do you keep a backup? Why use `|` as the delimiter in a path replacement?  🎯
5. In `awk`, what are `$0` and `$1`, and what does `-F` do? What’s the difference between `print $1 $7` and `print $1, $7`? Write a command to print the 2nd column of a comma-separated file.  🎯
6. `cut -d, -f1,3 data.csv`: what does it do? What is `cut`’s default delimiter? When would you pick `awk` over `cut`?🎯

**Sorting, counting, splitting**  
7. Why must you `sort` before `uniq`? Write the pipeline that shows the most frequent lines in `errors.log` first. What does `sort -k 3` do, and why add `n`?  🎯
8. `paste` vs `join` vs `cat`: how does each combine files? What must be true of the inputs to `join`?  🎯
9. Write the command to split `big.csv` into chunks of 100,000 lines with the prefix `part_`, then rejoin them, then verify the line counts.

---
NOT DONE

10. What do `wc -l`, `-w`, `-c`, and `-m` count? Write a command that counts the files in a folder.

**Patterns and cleaning**  
11. What do `.`, `*`, `^`, and `$` mean in a regex? Explain `..$`, `^..`, and `l.*y`. Why does `grep 'b.|j.'` fail, and how do you fix it?  
12. What do `tr a-z A-Z`, `tr -d 'z'`, `tr -s '[:space:]'`, and `tr -cd '[:digit:]'` do? Why can’t `tr` take a filename, and how do you feed it one? Write the command that removes Windows `\r` line endings.  
13. What does `tee` do, and what’s the name’s origin? Write a command that runs `python train.py`, shows its output live, and saves it (errors included) to `run.log`. Why does `echo "x" | sudo tee /etc/file` work when `sudo echo "x" > /etc/file` doesn’t?

**Capstone scenario**  
14. You SSH into a server with a 2 GB `train.log`. Write the commands to: (a) watch new lines live, (b) show ERROR lines with 2 lines of context, (c) count the ERROR lines, (d) save the ERROR lines to `errors.txt` while still seeing them.

**Bonus (VM, 1 minute):** run these and predict the output before you press Enter:

bash

```bash
seq 1 20 > nums.txt
head -3 nums.txt
wc -l nums.txt
split -l 5 nums.txt part_ ; ls part_*
echo "a b b a a" | tr ' ' '\n' | sort | uniq -c | sort -nr
```

Which questions do they relate to? (Delete the files afterward with `rm nums.txt part_*`.)

### Answer key

1. `cat` prints a file, `tac` prints its lines in reverse order. `>` overwrites, `>>` appends. Heredoc:

bash

```bash
cat > config.yaml << EOF
lr: 0.001
epochs: 10
EOF
```

Input ends at the `EOF` line. In plain `cat > file`, press `Ctrl+D`. (`echo -e` enables `\n` and `\t`, and `echo $VAR` prints a variable.)  
2. `head -n 5 data.csv` (or `head -5`), `wc -l data.csv`, and `zgrep -i error train.log.gz`. Other tools in the family: `zcat`, `zless`, `zdiff`, plus `xzcat` and `xzless` for `.xz` files.  
3. `-v` inverts (shows non-matching lines), `-C 3` shows 3 lines before and after each match, and `-c` counts matching lines. `grep -C 3 "CUDA out of memory" train.log` and `grep -v '^#' file | grep -v '^$'`.  
4. Without `g`, only the first match on each line is replaced, and with `g` every match is replaced. Neither changes the file, since sed prints the result. `-i` edits the file in place, and `-i.bak` keeps a backup. Preview first, then add `-i`. `|` (or `#`) avoids escaping slashes: `sed 's|/old/path|/new/path|g'`.  
5. `$0` is the whole line, `$1` is the first field, and `-F` sets the field separator. `print $1 $7` joins the fields with no space, and `print $1, $7` puts a space between them. `awk -F, '{print $2}' data.csv`.  
6. It extracts fields 1 and 3 from a comma-separated file. The default delimiter is a tab. `awk` handles runs of spaces automatically, while `cut` treats every single space as a separator, so use `awk` for column-aligned output like `ls -l` or `ps`.  
7. `uniq` only collapses adjacent duplicates, so identical lines must be next to each other. `sort errors.log | uniq -c | sort -nr`. `sort -k 3` sorts starting at field 3 (through the end of the line), and `-k 3,3` limits it to field 3 alone. Add `n` for numeric sorting, otherwise `10` sorts before `2`.  
8. `paste` puts files side by side line by line (`-d,` sets the separator, `-s` serializes). `join` merges two files on a common field, and both must be sorted on that field. `cat` joins files one after the other.  
9. `split -l 100000 big.csv part_`, then `cat part_* > restored.csv`, then `wc -l part_*` to check the counts. This is how you shard a big dataset.  
10. `-l` lines, `-w` words, `-c` bytes, `-m` characters. `ls | wc -l` counts entries in a folder.  
11. `.` matches any single character, `*` means zero or more of the previous item, `^` is the start of a line, and `$` is the end. `..$` matches the last two characters, `^..` the first two, and `l.*y` an `l`, anything, then a `y`. `|` (alternation) needs extended regex, so use `grep -E 'b.|j.'`.  
12. Uppercases text, deletes every `z`, squeezes repeated whitespace, and keeps only digits. `tr` reads only standard input, so use `<` or a pipe: `tr -d '\r' < in.txt > out.txt`. Windows line endings in a script cause errors like “bad interpreter” on Linux, so this fix is useful.  
13. `tee` is named after the T-shaped pipe fitting: it sends output to both the screen and a file. `python train.py 2>&1 | tee run.log` (`-a` appends). In `sudo echo "x" > file`, your own shell does the redirect, so `sudo` doesn’t apply to it. With `| sudo tee`, `tee` itself runs as root.  
14. (a) `tail -f train.log` (b) `grep -C 2 ERROR train.log` (c) `grep -c ERROR train.log` (d) `grep ERROR train.log | tee errors.txt`.

**Bonus:** `head` and `wc -l` relate to question 2 and question 10, `split` to question 9, and the last pipeline to question 7. It prints `3 a`, then `2 b`, so the most frequent line comes first.