---
layout: page
---

# CH 10 | Potpourri


### Keyboard remapping

* Use xmodmap or AutoKey

### Daemons

```Bash
"Most computers have a series of processes that are always running in the background rather than waiting for an user to launch them and interact with them. These processes are called daemons and the programs that run as daemons often end with a d to indicate so."

  systemctl start <daemon>    # Start a service   
  systemctl stop <daemon>     # Stop a service
  systemctl restart <daemon>  # Restart a service 
  systemctl status <daemon>   # Check status of a service
  systemctl enable <daemon>   # Start a service on boot-up
  systemctl disable <daemon>  # Don't start a service on boot-up

  # Example Daemon
  # /etc/systemd/system/myapp.service
  [Unit]
  Description=My Custom App
  After=network.target

  [Service]
  User=foo
  Group=foo
  WorkingDirectory=/home/foo/projects/mydaemon
  ExecStart=/usr/bin/local/python3.7 app.py
  Restart=on-failure

  [Install]
  WantedBy=multi-user.target
```

### FUSE

```bash
"FUSE (Filesystem in User Space) allows filesystems to be implemented by a user 
program. FUSE lets users run user space code for filesystem calls and then 
bridges the necessary calls to the kernel interfaces. In practice, this means 
that users can implement arbitrary functionality for filesystem calls.

For example, FUSE can be used so whenever you perform an operation in a virtual 
filesystem, that operation is forwarded through SSH to a remote machine, performed
there, and the output is returned back to you. This way, local programs can see
the file as if it was in your computer while in reality it’s in a remote server."


  sshfs      # Open locally remote files/folder through an SSH connection.
  rclone     # Mount cloud storage services like Dropbox, GDrive, Amazon S3 or Google Cloud Storage and open data locally.
  gocryptfs  # Encrypted overlay system. Files are stored encrypted but once the FS is mounted they appear as plaintext in the mountpoint.
  kbfs       # Distributed filesystem with end-to-end encryption. You can have private, shared and public folders.
  borgbackup # Mount your deduplicated, compressed and encrypted backups for ease of browsing.
```

### Backups

* (Discussion from 2019)[https://missing.csail.mit.edu/2019/backups/]

* Version Control != Backup

### APIs

* Application Programming Interfaces (APIs) let developers interact with web-hosted services programatically
* Use `curl` or a library (like `Requests`) to make calls to APIs
* Use authentication protocals (like OAuth) to access secured APIs

### Common command-line flags/patterns

```bash

  --help      # Help
  --version   # Version
  --quiet     # No output
  --verbose   # More output
  -r          # Recursive
  --          # Stop processing flags (i.e. rm -- -r deletes a directory named "-r")

```

### Window managers

* Floating (drag-and-drop) vs. Tiling (keyboard shortcuts)

### VPNs

[Discussion from 2019](https://missing.csail.mit.edu/2019/security/)

* Virtual Private Networks (VPNs) keep your information private from Internet Service Providers (ISPs), at the expense of exposing that information to the VPN hoster
* Web traffic is already secured by HTTPS/SSL
* Wireguard can be used to "roll your own" personal VPN, as opposed to renting a service

### Markdown

* ...is what I'm writing these notes with
* More detailed than .txt, less detailed than .docx

### Hammerspoon(desktop-automation-on-macOS)

* System automation for Mac's (written in Lua)

### Booting + Live USBs

* Live USB's are pluggable drives you can boot into 
* Helpful for troubleshooting failed systems

### Docker, Vagrant, VMs, Cloud, OpenStack

* **Virtual Machines (VMs)** are emulated computers, run within a computer
* **Vagrant** can be used to create virtual machine templates with preinstalled software/configurations
* **Docker** can create lightweight "containers", that function as mini-VMs for a specific application or program
* **Cloud Services** like Azure and AWS can rapidly provision VM's for use
* **OpenStack** is a cloud service setup for MIT students

### Notebook programming

* Useful for rapid prototyping and exploratory efforts
* Jupyter is one of the most popular tools for notebook programming

### GitHub

* Create an **Issue** on a repository to report problems
* Create a **Fork** of a repository to develop it separate from the original
* Create a **Pull Request** to have the repository owner review changes you would like to make to their code
