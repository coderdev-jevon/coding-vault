# Chap 6: Common Linux Applications
Date: 2026-08-15

## * Internet Applications
#### ** Web Browsers
- ==Firefox: open source==
- ==Google Chrome & Microsoft Edge: proprietary==
- ==Chromium: open source chrome==
- GNOME Web (Epiphany)
- Opera
- `Konqueror`
- Text-based browsers

#### ** Email Clients
**3 Standard Mail Protocols:**
1. ==IMAP==: Saves email on mail server and sync between all your devices, modern, receive
2. POP3: Downloads emails onto local computer
3. ==SMTP==: Used for sending outgoing emails (opposite of incoming emails), send
**Graphical Email Clients:**
- Thunderbird
- Evolution
- Claws Mail
**Text-based Email Clients:**
- Mutt
- mail
**Web-based Email Services:**
- Google
- Yahoo Mail
- Microsoft Outlook/Office 365

#### ** File Transfer Tools
- Secure File Transfer Protocol (SFTP)
- FTP Secured (FTPS)

#### ** Messaging and Conferencing Applications
- Pidgin
- `Hexchat`

## * Productivity and Development Applications
#### ** ==LibreOffice==
LibreOffice is the standard office suite in Linux, can read and write Microsoft Office file formats.
Office suite - several office applications bundled together

Aside from LibreOffice, ONLYOFFICE can be a choice

1. Writer - word processor
2. Calc - spreadsheet application
3. Impress - presentation tool
4. Draw- vector graphics and diagram editor
5. Base - database frontend
6. Math - formula editor for creating mathematical and scientific notation
#### ** Editors
- ==VS Code==
- ==VS Codium==
- vim
- emacs

#### ** Compilers, Interpreters, and Runtimes
1. ==**Compilers**== -> take all source code and translate into machine code
	source code -> compiler -> executable binary file -> run
	GCC and Clang for C, C++
2. ==**Interpreter**== -> read line by line, translate, and execute immediately
	source code -> interpreter -> run directly line by line
	Python, Bash shell script
3. **==Runtimes (Runtime Environment)==**  -> bundles of supporting libraries, tools, and services to execute your program
Sometimes a program is not converted directly to raw machine code, but only to intermediate format that only runtime understands

Example: Go, Rust, Java, Ruby, Node.js

#### ** ==Debuggers==
A tool to pause your program, inspect what's happening, all to find bugs (set breakpoints)

Example: GDB for C, C++, `Valgrind`

#### ** ==Version Control==
The system that track change you make to files.

Example: Git, SVN

#### ** ==Containers==
Only works on a Linux host, its like private room that has its own furniture inside one main big house (host).

Example: Docker, `Podman`

#### ** ==Integrated Development Environments (IDEs)==
It is an all-in-one program for writing code. Text editor, compiler/interpreter, debugger, file manager all is inside IDE.

Example: Eclipse, Visual Studio Code, JetBrains


## * Examining Installed Applications
#### ** Distinguish `apt` or `snap` installed
1. `snap list APP_NAME` to check
2. Go to GNOME Software -> Installed tab -> Label written Snap = Snap
3. All in Synaptic Package Manager are APT packages.

```
snap refresh APP_NAME # update
snap remove APP_NAME # uninstall
```

```
sudo apt update
sudo apt upgrade # upgrade/repair packages
sudo apt remove APP_NAME
```


