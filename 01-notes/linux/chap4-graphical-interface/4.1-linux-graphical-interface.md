# Chap 4: Graphical Interface
Date: 2026-08-13

## * Desktop Environment
In windows, desktop is permanently built into OS, just like a kitchen with a fixed layout. In Linux, desktop is not a part of core OS, it is separated software called as Desktop Environment (DE), like an empty kitchen in which you can install any layout you want. 

GNOME is widely used desktop environment in Linux.
#### ** Desktop Environment Three Core Components
1. Session manager, starts and maintains elements of graphical session
2. Window manager, how windows are displayed on screen
3. A set of utilities and applications

#### ** Two Types of Session in Ubuntu
Wayland system (modern window system) and X11 (`Xorg`) window system (old)

`Log out by clicking button of the top right corner`


## * Session Management
#### ** Lock the Screen
Lock screen by click icons in upper-right-corner on GNOME desktop environment and look for lock option, app still running in the background.

or

`Super + L / Windows + L / Windows + Escape`

If you want to change shortcut settings, go to app -> settings -> Keyboard -> View and Customize Shortcuts

#### ** Switching Users
In Linux, it is fundamental to allow multi-user in a single system, just go switch user in the login screen.

#### ** Shutting Down and Restarting
Proper shutdown process will save you from lost of unsaved data and file system corruption. Make sure to save your data and do shutdown on GNOME properly.

#### ** Suspending the System
Suspend is equal to sleep mode in Windows, it's good if you want to leave your screen while keeping all activities intact, better option that rebooting again later on, almost all activities are paused.


## * Basic Operations
#### ** Launching Applications
To search for applications just type directly to search or click App icon at bottom-left corner

#### ** Viewing Files and Directories
You can switch between display view inside file manager by icon in toolbar or by `Ctrl + 1 and Ctrl + 2`

Press `Ctrl + H` to view hidden files that begin with period(.), usually configuration data

#### ** Searching Files
To search for files you can go to toolbar or `Ctrl + F`

To navigate to known directory path, you can press `Ctrl + L`

**Nautilus** provides built-in search tool that include filter options.

#### ** Editing a File
To create a file, go to terminal and type `touch filename`, `gedit` is default text editor in GNOME.

#### ** Deleting a File
To delete a file, you can press `Ctrl / Shift` to select multiple files, then press `del` key.

Trash folder is located at `./loca/share/Trash/files`, right click Trash in left panel and select Empty Trash to delete all files there.

#### ** Creating Text Files
You can create file by text editor app and save it