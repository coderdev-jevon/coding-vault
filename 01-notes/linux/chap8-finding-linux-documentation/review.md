### Questions

**Choosing the right source**

1. Match each to its best use: `--help`, `man`, `info`, `help`. 🎯
2. Why does `help cd` work but `cd --help` doesn’t? What kind of command is `cd`? 🎯
3. You forgot a command’s name but know it’s about disk usage. What do you run? Then, once you know the name, what do you run to see its quick options?
4. `man -f passwd` vs `man -k passwd`: what’s the difference? Name the equivalent command for each.

**Man pages (most important)**  
5. What do man chapters 1, 5, and 8 contain? Which two chapters will matter most when you start programming in C?  
6. `man passwd` and `man 5 passwd` show different pages. Why? How do you browse every chapter’s page for a name?  
7. Inside a man page, which keys do you use to scroll a page, search, and quit? (Think of the `less` lesson.)

**Info and other sources**  
8. What is a node in `info`? Which keys move to next, previous, and parent node, and how do you search?  
9. Menu link vs named link in `info`: how does each look?  
10. Where is package documentation stored? How do you read a `.gz` file there without extracting it?

**Scenario**  
11. A training script on a remote server fails with “unrecognized option.” What’s your fastest two-step lookup?

**Bonus (VM, 1 minute):** run `man 5 passwd`, `help cd`, and `ls /usr/share/doc | head`. Which questions do they relate to?

### Answer key

1. `--help` is a quick reminder of options and syntax. `man` is the standard manual for commands and tools. `info` is deeper, tutorial-style documentation. `help` covers shell built-in commands.
2. `cd` is a shell built-in, not a separate program, so it has no `--help` option of its own. Built-ins are documented with `help`.
3. `man -k disk` (or `apropos disk`, which means related to) searches manual descriptions for the keyword. Then `command --help` for a quick look at its options.
4. `man -f passwd` (same as `whatis passwd`) finds pages whose name exactly matches and shows a one-line description. `man -k passwd` (same as `apropos passwd`) lists every page that mentions the keyword.
5. 1 is user commands, 5 is configuration file formats, 8 is admin commands. For C, chapter 2 (system calls) and chapter 3 (library functions) are the ones you’ll open all the time.
6. The same name can exist in several chapters. `man passwd` shows chapter 1 (the command), while `man 5 passwd` shows chapter 5 (the `/etc/passwd` file format). `man -a passwd` browses all of them.
7. Space scrolls down a page, `b` goes back, `/word` searches, and `q` quits (the same keys as `less`).
8. A node is a section of the document, like a chapter in a book. `n` is next, `p` is previous, `u` is up to the parent, `/` searches, and `h` shows help.
9. Menu links start with `*` and end with `::`, and they live in a menu list. Named links appear inside paragraphs and end with `::`.
10. `/usr/share/doc`. Use `zless filename.gz` to read compressed files directly.
11. `command --help` for the valid options, then `man command` if you need the details.

**Bonus:** `man 5 passwd` relates to questions 5 and 6, `help cd` to question 2, and `ls /usr/share/doc | head` to question 10.

## ==* `whatis`, `man -k`, `apropos`==
`whatis` only search for exact match, while `man-k` and `apropos` search for identicals.