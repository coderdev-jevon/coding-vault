# Chap 8: Finding Linux Documentation

## * Linux Documentation Sources
Include `man` pages, GNU Info, `help` command and `--help` option, other documentation like [Ubuntu Documentation](https://help.ubuntu.com/community/CommunityHelpWiki)

## ==* `man` pages==
It provides documentation for programs, utilities, and topics.
```bash
man program
```

Not limited inside Linux terminal, there are also online formats and PDFs, even technical books.

[Linux man pages online](https://man7.org/linux/man-pages/)


## * When to Use Them?
==Use `-h` or `--help` for quick reminder of basic options, flags, syntax==
==Use `man` for standard manual page, good for CLI tools, commands==
==Use `info` for detailed, tutorial, deep learning==
==Use `help` for built-in commands==

## * `man`
#### ==** `man -f`==
Look for man pages whose name exactly match your topic
```bash
man -f passwd
whatis passwd
```

#### ==** `man -k`==
List for all manuals that talk about your keyword
```bash
man -k passwd
apropos passwd
```

## ==* `man` Chapters==
```plaintext
1 = user commands 
2 = system calls 
3 = library functions 
4 = device files 
5 = configuration file formats 
6 = games 
7 = misc / guides 
8 = admin commands
9 = kernel internal routines (developer-only)
```

```bash
man N name # open only chapter N
man -a name # browse all chapters
```

## ==* GNU Info System==
It is alternative to `man`. It seems outdated but it is more a complete choice.

```bash
info # browse through topics

info <topic_name>
```

`info` content is split between nodes, nodes is like chapters inside a book. `info` is hyperlinked document with nodes and clickable links, just a website.

#### ==** Two Types of Links==
1. **Menu Links**, start with `*` and ends with `::`, which live inside a menu list
2. **Named Links**, no leading `*`, ends with `::`, appear inside paragraphs.

#### ==** Keys and Function==
```bash
n # next node
p # previous node
u # move to parent node
/ # for searching
h # for help
```

## ==* `--help` Option==
Really great for quick reference
```bash
man --help 
man -h 
```

```bash
help name # can also be used as another alternative
```


## * Other Documentation Sources
1. ==**Desktop/Graphical help system**==
	look for ? icon or `gnome-help` or `yelp`
2. ==**Package documentation**==
	it is under `/usr/share/doc`, and look for packages, then run `zless` for `.gz` files or just run ``
3. ==**Online resources**==
	read distribution documentation or look for well-reviewed courses.

## ==* How to open `man` and `info` on GNOME-GUI==
1. Run `gnome-help` on terminal
2. Then press `CTRL + l`
3. Lastly, type desired manual or info you would like to find
