
# Chap 12.2: Environment Variables
Date: 2026-10-05

## * Environment Variables
Environment variables are ==quantities that have specific values== (can be preset or set directly by user) which may be utilized by command shell.

To ==look at environment variables available==
```bash
set # local and environment variables
env # only environment variables
export # move local to environment
	export EDITOR=vim
	export EDITOR
```

## * ==Setting Environment Variables==
Local variables are not available to child processes.

```bash
echo $HOME # to look at the value of the variable
export VARIABLE=value; export VARIABLE
```

#### ==** Add variables permanently==
==Edit `~/.bashrc`== and add the line `export VARIABLE=value`
Lastly ==start a new shell==
```bash
source ~/.bashrc
. ~/.bashrc
bash
```

#### ==** Add Environment Variables to Specific Process==
```bash
SDIRS="s_0*" KROOT=/lib/modules/$(uname -r)/build make modules_install
```
Add SDIRS and KROOT environment variables to command `make modules_install`

#### ==** Temporary Environment Variables vs Local Variables==
Environment variables are shared to every child processes, while local variables is only specific to a shell. 

They both die when sessions end by closing the terminal or `exit`.

## ==* The HOME Variable==
```bash
cd $HOME
cd ~
```

#### ** Additional Commands
```bash
pwd # find out present directory
```

## ==* The PATH Variable==
It is a ==list of all the directories==, which will be used for command like `ls`.

`:` shows different directory

Null directory shows current directory.ex

```bash
:path1:path2 # null directories before first colon
path1::path2 # null directory between path1 and path2
```

Fix this variable if terminal says "command not found".
```bash
export PATH="$PATH:/home/you/tools/bin"
```
#### ==** Make the PATH Variable Fix Permanent==
Go to `~/.bashrc` and add line there.

## * The SHELL Variable
```bash
$SHELL # the location of the shell program you're using
```

## * The PS1 Variable and the Command Line Prompt
Prompt is the text the terminal shows you before the cursor.
==`PS1` stands for Prompt String 1==

```bash
\u # user name
\h # host name
\w # current working directory
\! # history number of this commmand
\d # date

OLD_PS1=$PS1
export PS1='\u@\h:\w$ '
```

## ==* Simple Application of $PATH==
```bash
echo "echo HELLO, this is the phony ls program" > /tmp/ls
chmod +x /tmp/ls # make it executable

#try both
export PATH="$PATH:/tmp/ls" # append
export PATH="/tmp/ls:$PATH" # prepend

which ls # try for both

rm /tmp/ls
```

