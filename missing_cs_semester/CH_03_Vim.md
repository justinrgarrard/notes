---
layout: page
---

# CH 3 | Editors (Vim)

### Basic Philosophy: You Read More Than You Write

```bash
# Mode-based Editing
	Normal (Esc)        # for moving around a file and making edits
	Insert (Esc + i)    # for inserting text
	Replace (Esc + R)   # for replacing text
	Visual (Esc + v)    # for selecting blocks of text
	Command-line (:)    # for running a command
```

```bash
# Basic Commands
    :q quit             # (close window)
    :w save             # (“write”)
    :wq                 # save and quit
    :e {name of file}   # open file for editing
    :ls                 # show open buffers
    :help {topic}       # open help
        :help :w        # opens help for the :w command
        :help w         # opens help for the w movement
```

```bash
# Movement
    Basic movement: hjkl        # (left, down, up, right)
    Words:  w # (next word)
            b # (beginning of word)
            e # (end of word)
    Lines:  0 # (beginning of line)
            ^ # (first non-blank character)
            $ # (end of line)
    Screen: H # (top of screen)
            M # (middle of screen)
            L # (bottom of screen)
    Scroll: Ctrl-u # (up)
            Ctrl-d # (down)
    File:   gg # (beginning of file)
            G # (end of file)
    Line numbers:   :{number}<CR>
                    {number}G (line {number})
    Misc: % (corresponding item)
    Find:   f{character} # find/to forward/backward {character}
            t{character}
            F{character}
            T{character}
            , / ; # for navigating matches
    Search: /{regex}
            n / N # for navigating matches
```

```bash
# Editing
    i           # enter insert mode
    o / O       # insert line below / above
    d{motion} 
    delete {motion}
        # e.g. dw is delete word, d$ is delete to end of line, d0 is delete to beginning of line
    c{motion}
    change {motion}
        # e.g. cw is change word like d{motion} followed by i
    x delete character      # (equal do dl)
    s substitute character  # (equal to xi)
    visual mode + manipulation
        # select text, d to delete it or c to change it
    u           # to undo
    <C-r>       # to redo
    y           # to copy / “yank” (some other commands like d also copy)
    p           # to paste
    ~           # flips the case of a character
```

```bash
# Getting Fancy
    3w      # move 3 words forward
    5j      # move 5 lines down
    7dw     # delete 7 words


    ci (    # change the contents inside the current pair of parentheses
    ci [    # change the contents inside the current pair of square brackets
    da\'    # delete a single-quoted string, including the surrounding single quotes
```

``` bash
# Search and Replace
    :s # (substitute) command (documentation).

    %s/foo/bar/g
        # replace foo with bar globally in file
    %s/\[.*\](\(.*\))/\1/g
        # replace named Markdown links with plain URLs
```

``` bash
# Multiple Windows
	:sp / :vsp  # to split windows
```
