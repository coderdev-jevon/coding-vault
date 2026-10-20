### Questions

**Choosing an editor**

1. Why isn’t Word a text editor? What would go wrong if you edited a config file or script in it? 🎯
2. Which of the five editors are terminal-based, and which are graphical? Which would you expect to find on a server with no desktop, and why is `vi` worth learning even if `nano` feels easier? 🎯
3. In `nano`, how do you open a file, save it, and exit? (Your Chapter 10 notes have the keys.) 🎯

**vi basics**  
4. What are the main modes in `vi`? Which key returns you to Normal mode? Name the five keys that start typing: `i`, `a`, `A`, `o`, `O`.  🎯
5. How do you quit without saving? How do you save and quit? (One of these isn’t in your notes yet, so recall it from `vimtutor`.)  🎯
6. What do `x`, `dw`, `d$`, `dd`, and `3dd` do? Write the general command syntax and say what `c` does differently from `d` (`ce`, `cc`).  v
7. How do you copy a line, paste it, undo the last change, restore a whole line, and redo?  🎯
8. What do `gg`, `G`, `45G`, `0`, `$`, `%`, and `Ctrl+G` do?🎯

**Search and replace**  
9. How do you search forward and backward? How do you repeat the search, and how do you jump back to where you were?  🎯
10. Explain every part of `:%s/old/new/gc`. What changes if you drop `%`? If you drop `g`?🎯

**External commands and files**  
11. Scenario: you’re editing a file in vim and want to run `ls` without leaving the editor, then paste its output into the file. Then you decide to leave without keeping your changes. Write the commands for all three steps.  🎯
12. How do you save only some lines to another file? What is the difference between `w` and `w!` there?  🎯
13. How do you open vim’s help and close the help window? Why are many vim features “off” by default, and what file turns them on?

**Bonus (VM, 1 minute):** run `which nano vi vim` and then `vimtutor`. Do lesson 1 and 2 with your fingers. Which questions do they relate to?

### Answer key

1. Word is a word processor. It stores formatting (fonts, colors) and hidden data in the file, so a config file or script saved from it contains extra content that breaks the program reading it. A text editor stores only the characters you type.
2. Terminal-based: `nano`, `vi`/`vim`, and `emacs` (text mode). Graphical: `gedit` and VS Code (`vi` and `emacs` also have graphical forms). On a server with no desktop you’d use `nano` or `vi`. `vi` is the standard tool installed on nearly every distribution, so it’s the one you can count on being there.
3. `nano filename`. `Ctrl+O` writes the file out (press Enter to confirm the name), and `Ctrl+X` exits.
4. Normal mode (keys are commands), Insert mode (keys type text), Visual mode (selecting, with `v`), and command-line mode (starts with `:`). `Esc` returns to Normal mode. `i` inserts before the cursor, `a` after it, `A` at the end of the line, `o` opens a new line below, and `O` opens one above.
5. `:q!` quits and discards changes. `:wq` saves and quits (`ZZ` and `:x` do the same).
6. `x` deletes the character under the cursor, `dw` deletes a word, `d$` deletes from the cursor to the end of the line, `dd` deletes the whole line, and `3dd` deletes 3 lines. Syntax is `[count] operator [count] motion`. `c` works like `d` but then puts you in Insert mode: `ce` changes to the end of the word, and `cc` changes the whole line.
7. `yy` copies the line (`yw` copies a word), `p` pastes, `u` undoes the last change, `U` restores the whole line to its original state, and `Ctrl+R` redoes.
8. `gg` is the start of the file, `G` is the end, `45G` is line 45, `0` is the start of the line, `$` is the end of the line, `%` jumps to the matching parenthesis, and `Ctrl+G` shows file location and status.
9. `/word` searches forward and `?word` searches backward. `n` repeats in the same direction, `N` in the opposite direction, and `Ctrl+O` jumps back to the earlier position (`Ctrl+I` goes forward again).
10. `:` is command mode, `%` means every line, `s` is substitute, `old`/`new` are the text, `g` means all matches on each line, and `c` asks for confirmation each time. Without `%`, only the current line changes. Without `g`, only the first match on each line changes.
11. `:!ls` runs `ls` and returns to the editor. `:r !ls` inserts the output of `ls` into the file. `:q!` quits and discards changes.
12. Press `v`, move to select the lines, then type `:`, which auto-fills `:'<,'>`, add `w TEST` and press Enter. `w` fails if `TEST` already exists, and `w!` overwrites it.
13. Press `F1` or type `:help`. `Ctrl+W` jumps between windows, and `:q` closes the help window. Vim has more features than vi, but most are disabled until you create a `vimrc` file (usually `~/.vimrc`).

**Bonus:** `which nano vi vim` shows which editors exist on your machine (question 2), and `vimtutor` practices questions 4 to 8. If `vim` isn’t found, `sudo apt install vim` gets the full version.