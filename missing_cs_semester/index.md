---
layout: page
---

# Missing CS Semester Notes

https://missing.csail.mit.edu/

* [CH 01 The Shell](CH_01_Shell.md)
* [CH 02 Shell Tools and Scripting](CH_02_Scripting.md)
* [CH 03 Editors (Vim)](CH_03_Vim.md)
* [CH 04 Data Wrangling](CH_04_Data_Wrangling.md)
* [CH 05 Command-line Environment](CH_05_CLI.md)
* [CH 06 Version Control (Git)](CH_06_Git.md)
* [CH 07 Debugging and Profiling](CH_07_Debug.md)
* [CH 08 Metaprogramming](CH_08_Metaprogramming.md)
* [CH 09 Security and Cryptography](CH_09_Security.md)
* [CH 10 Potpourri](CH_10_Potpourri.md)

### Linux Tools Reference

```bash
# Common Tools
    vim         # Terminal text editor
    grep        # Finds strings in text.
    sed         # Stream editor; manipulates inputs.
    less        # Paginates outputs.
    sort        # Sorts output.
    uniq        # Narrows down to unique outputs.
    tail        # Displays the bottom of a file.
    awk         # Processes inputs as delimited fileds.
    wc          # Count lines, words, or bytes
    paste       # Merge lines of files.
    bc          # Calculator
    xargs       # Execute another command using piped inputs.
    curl        # Make a web request, without a browser.
    ffmpeg      # Video/image converter.

# Resource Monitors
    ## GENERAL
        top/htop    # High-level overview of system performance
        gotop       # Prettier version of htop
        glances     # Prettier version of htop
        dstat       # Line-by-line updated statistics

    ## DISK
        iotop       # I/O usage metrics
        df/du       # Check disk space usage
        ncdu        # TUI interface for checking disk space usage
        lsof        # List open files

    # MEMORY
        free        # Shows free and used memory
        jps         # Shows Java processes

    # Network
        wireshark   # Traces network traffic
        ss          # Shows active ports, replaces netstat
        ip          # Shows active interfaces, replaces ifconfig
        nethogs     # Similar to wireshark
        iftop       # Similar to wireshark

# Daemon Control
    systemctl start <daemon>    # Start a service   
    systemctl stop <daemon>     # Stop a service
    systemctl restart <daemon>  # Restart a service 
    systemctl status <daemon>   # Check status of a service
    systemctl enable <daemon>   # Start a service on boot-up
    systemctl disable <daemon>  # Don't start a service on boot-up

# Job Control
    ps -aux     # List processes
    CTRL+C      # Job Interrupt
    CTRL+/      # Job Quit
    CTRL+Z      # Job Stop
    kill <pid>  # Job Terminate

# Basic Git
    git clone               # download repository from remote
    git pull                # same as git fetch; git merge
    git init                # creates a new git repo, with data stored in the .git directory
    git status              # tells you what’s going on
    git add <filename>      # adds files to staging area
    git commit              # creates a new commit
    git push <remote> <local branch>:<remote branch>        
        # send objects to remote, and update remote reference

# Specialized Tools
    strace      # Traces system calls and signals
    perf        # A fancier version of strace
    hyperfine   # A benchmark tool for CLI programs
    tcpdump     # Dumps network traffic
    telnet      # Checks network ports
    wireshark   # Traces network traffic
    browser     # Has developer tools for monitoring code, network, and storage (F12 usually)
    Selenium    # A common testing/automation framework for web browsers
    stress      # Create artificial load on the system
```