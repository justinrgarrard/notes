---
layout: page
---

# CH 7 | Debugging and Profiling

### Debugging

* **Print Statements** are easy to implement

* **Logging Systems** take a little more work, but are more durable and flexible
  * Many Linux applications store their logs at `/var/log`
  * Linux daemons store their logs at `/var/log/journal`, which can be queried with `journalctl`
  * The `logger` command can make entries in `/var/log/journal`

* **Static Analysis** can find errors before code is run
  * Also referred to as "linters", similar to lint rollers cleaning clothes

* **Debuggers** can pause execution of code and inspect variable values
  * These tend to be programming language specific

* **Specialized Tools** are less easy to use, but can debug just about anything

```
Specialized Tools

    strace      Traces system calls and signals
    perf        A fancier version of strace
    hyperfine   A benchmark tool for CLI programs
    tcpdump     Dumps network traffic
    telnet      Checks network ports
    wireshark   Traces network traffic
    browser     Has developer tools for monitoring code, network, and storage (F12 usually)
    Selenium    A common testing/automation framework for web browsers
    stress      Create artificial load on the system
```

### Profiling

* Monitors and measures performance

* Code profiliers are often specific to programming languages

```
Code Profilers

    time            A Python module that takes millisecond timestamps
    cProfile        A Python module that measures CPU time taken per function
    line_profiler   A Python module that measures CPU time taken per function, per line
    memory-profiler The Python equivalent of Valgrind; detects memory usage in code
```

* Resource monitors fulfill a similar purpose on a system-level

```
Resource Monitors

    GENERAL
        top/htop    High-level overview of system performance
        gotop       Prettier version of htop
        glances     Prettier version of htop
        dstat       Line-by-line updated statistics

    DISK
        iotop       I/O usage metrics
        df/du       Check disk space usage
        ncdu        TUI interface for checking disk space usage
        lsof        List open files

    MEMORY
        free        Shows free and used memory
        jps         Shows Java processes

    Network
        wireshark   Traces network traffic
        ss          Shows active ports, replaces netstat
        ip          Shows active interfaces, replaces ifconfig
        nethogs     Similar to wireshark
        iftop       Similar to wireshark
```

