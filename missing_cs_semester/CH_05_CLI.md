---
layout: page
---

# CH 5 | Command Line Interface

### Job Control

```bash
# Signals

    CTRL+C      # Job Interrupt
    CTRL+/      # Job Quit
    CTRL+Z      # Job Stop

    kill <pid>  # Job Terminate
```

```bash
# Running Processes

    jobs        # List jobs
    ps -aux     # List processes
    fg <job_id> # Move job to foreground
    bg <job_id> # Move job to background
```

### Terminal Multiplexers

* Allow one terminal to act as multiple terminals
* Most popular tool is tmux
* CTRL+b = \<C-b>

```bash
# tmux Sessions

"A session is an independent workspace with one or more windows"

    tmux starts a new session.
    tmux new -s NAME starts it with that name.
    tmux ls lists the current sessions
    Within tmux typing <C-b> d dettaches the current session
    tmux a attaches the last session. You can use -t flag to specify which
```

```bash
# tmux Windows

"Equivalent to tabs in editors or browsers, they are visually separate parts of
the same session"

    <C-b> c     # Creates a new window. To close it you can just terminate the shells doing <C-d>
    <C-b> N     # Go to the N th window. Note they are numbered
    <C-b> p     # Goes to the previous window
    <C-b> n     # Goes to the next window
    <C-b> ,     # Rename the current window
    <C-b> w     # List current windows
```

```bash
# tmux Panes

"Like vim splits, pane let you have multiple shells in the same visual display."

    <C-b> \"            # Split the current pane horizontally
    <C-b> %             # Split the current pane vertically
    <C-b> <direction>   # Move to the pane in the specified direction. 
                        # Direction here means arrow keys.
    <C-b> z             # Toggle zoom for the current pane
    <C-b> [             # Start scrollback. You can then press <space> to start 
                        # a selection and <enter> to copy that selection.
    <C-b> <space>       # Cycle through pane arrangements.
```

### Aliases

* Shortcut commands for common operations
* Whitespace-sensistive

`alias ll=ls -l`

### Dotfiles

* Hidden files that represent application configurations

```bash
# Dotfile Organization

"How should you organize your dotfiles? They should be in their own folder, 
under version control, and symlinked into place using a script. This has the 
benefits of:

    * Easy installation: if you log in to a new machine, applying your 
    customizations will only take a minute.
    * Portability: your tools will work the same way everywhere.
    * Synchronization: you can update your dotfiles anywhere and keep them 
    all in sync.
    * Change tracking: you’re probably going to be maintaining your dotfiles for
    your entire programming career, and version history is nice to have for 
    long-lived projects."
```

### Remote Machines

```bash
# SSH Basics

# SSH into a Remote Machine
ssh foo@bar.mit.edu

# Run a command on a remote machine
ssh foo@bar.mit.edu ls 

# Create an SSH key for automatic connections
ssh-keygen 
    ~/.ssh/id_rsa           ## SSH private key
    ~/.ssh/id_rsa.pub       ## SSH public key
    ~/.ssh/authorized_keys  ## List of approved clients

# Copy a file over SSH
scp path/to/local_file remote_host:path/to/remote_file

# Forward a port over SSH
ssh -L 9999:localhost:8888 foobar@remote_server
```

* Configure common SSH connections in `~/.ssh/config`.

```bash
# Example SSH Config

Host vm
    User foobar
    HostName 172.16.174.141
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
    RemoteForward 9999 localhost:8888

# Configs can also take wildcards
Host *.mit.edu
    User foobaz
```

* Configure server options for receiving SSH in `/etc/ssh/sshd_config`.

* Use `sshfs` to mount a local folder on a remote system


### Shells, Frameworks, and Terminal Emulators

* Bash | Zsh | Fish

* Augment your shell of choice with dotfiles and frameworks (like oh-my-zsh)

* Augment your terminal to tweak fonts, colors, etc.

