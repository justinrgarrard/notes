---
layout: page
---

# CH 1 | The Shell 

### The Shell

```bash
# Basics

    # This is a prompt
    missing:~$

    # This is a command, run from the prompt
    missing:~$ date
    Fri 10 Jan 2020 11:49:31 AM EST

    # The `PATH` variable shows where the system finds commands
    missing:~$ echo $PATH 
    /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

    # Running `pwd` Prints the Working Directory
    missing:~$ pwd
    /home/missing

    # Running `ls -l` shows files in the current directory with owners/groups
    missing:~$ ls -l
    drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing 
```

```bash
# File Permissions

    # File/directory permissions are represented like so:
    drwxr-xr-x

    # In an easier to read fashion:
    d  rwx  r-x  r-x

    d   # Can be "d" for directory or "-" for file
    rwx # The first three letters are for User permissions
    r-x # The next three letters are for Group permissions
    r-x # The last three letters are for everyone else (Other)

    # "r" for Read-Access
    # "w" for Write-Access
    # "x" for Execute-Access (required to enter directories)
```

```bash
# Pipes and Redirects

    # Use ">" to create new files (or overwrite) from output
    missing:~$ echo hello > hello.txt

    # Use "<" to feed inputs into a command
    missing:~$ cat < hello.txt
    hello

    # Use ">>" to append to files with output
    missing:~$ echo world >> hello.txt

    # Use "|" to chain output from one command into another
    missing:~$ ls -l / | tail -n1
    drwxr-xr-x 1 root  root  4096 Jun 20  2019 var
```

```bash
# Linux and Root

    # On Linux, everything is a file
    missing:~$ cd /sys/class/backlight/thinkpad_screen
    missing:thinkpad_screen$ echo 3 | sudo tee brightness

    # Critical files are often only accessible by "root", the system account
    # Commands executed "as root" can be done with `sudo`

    # When you switch users to become root, the prompt changes
    missing:~$ sudo su
    root:~#
```