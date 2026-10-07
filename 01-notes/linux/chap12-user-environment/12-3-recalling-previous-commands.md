
# Chap 12.3: Recalling Previous Commands
Date: 2026-10-05

## * Recalling Previous Commands
`bash` keep track of all commands in ==history buffer==, just use up and down cursor
```bash
history # look at previously executed commands
```

Information is stored in ==`~/.bash_history`==

## * ==Using History Environment Variables==
```bash
HISTFILE # location of history file
HISTFILESIZE # maximum number of lines in history file
HISTSIZE # maximum number of commands in history file
HISTCONTROL # how commands are stored
HISTIGNORE # which command lines can be unsaved
```

You can deep dive by learning from `man bash`

## * ==Finding and Using Previous Commands==
```bash
!! # execute the previous command 
CTRL-R # search previously used command, r stands for reverse-i-search
```

## ==* Executing Previous Commands==
```bash
! # start history substitution
!$ # refer to last argument in line
!n # refer to nth command line
!string # refer to most recent command starting with string
```

## ==* Keyboard Shortcuts==

![[linux-keyboard-shortcuts.png]]