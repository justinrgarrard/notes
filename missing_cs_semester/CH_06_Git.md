---
layout: page
---

# CH 6 | Version Control Systems (Git)

### VCS

* Tracks changes as a series of snapshots
* Records metadata on changes (who, what, when, where, why)
* Most common version control system is **git**


### Git's Data Model

```bash
# Terminology

    Tree = Directory
    Blob = File
    Snapshot = Commit
    Reference = SHA-1 Hash
    Repository = All Snapshots
```

```bash
# Example Repository

    top_dir/                (tree)
    ├── foo                 (tree)
    │   └── steve.txt       (blob)
    └── bar.txt/            (blob)
```

* The state of all components is captured in a **snapshot**
* Every tree, blob, and snapshot is an **object**
* Every object has a **reference** (SHA-1 pointer)
* The full collection of snapshots is a **repository**, and can be represented as a DAG (Directed-Acyclic Graph)


### References

* References are pointers to an object
* References can be:
  * An SHA-1 alphanumeric hash (ads2223114adfda)
  * A human-readable string ("master", "HEAD", "fred")


### Useful Commands

```bash
# Basics

    git help <command>      # get help for a git command
    git init                # creates a new git repo, with data stored in the .git directory
    git status              # tells you what’s going on
    git add <filename>      # adds files to staging area
    git commit              # creates a new commit
    git log                 # shows a flattened log of history
    git log --all --graph --decorate    # visualizes history as a DAG
    git diff <filename>                 # show differences since the last commit
    git diff <revision> <filename>      # shows differences in a file between snapshots
    git checkout <revision>             # updates HEAD and current branch
```

```bash
# Branching and merging

    git branch              # shows branches
    git branch <name>       # creates a branch
    git checkout -b <name>  # creates a branch and switches to it
                            # same as git branch <name>; git checkout <name>
    git merge <revision>    # merges into current branch
    git mergetool           # use a fancy tool to help resolve merge conflicts
    git rebase              # rebase set of patches onto a new base
```

```bash
# Remotes

    git remote                      # list remotes
    git remote add <name> <url>     # add a remote
    git push <remote> <local branch>:<remote branch>        # send objects to remote, and update remote reference
    git branch --set-upstream-to=<remote>/<remote branch>   # set up correspondence between local and remote branch
    git fetch                       # retrieve objects/references from a remote
    git pull                        # same as git fetch; git merge
    git clone                       # download repository from remote
```

```bash
# Undo

    git commit --amend      # edit a commit’s contents/message
    git reset HEAD <file>   # unstage a file
    git checkout -- <file>  # discard changes
```

```bash
# Advanced Git

    git config              # Git is highly customizable
    git clone --shallow     # clone without entire version history
    git add -p              # interactive staging
    git rebase -i           # interactive rebasing
    git blame               # show who last edited which line
    git stash               # temporarily remove modifications to working directory
    git bisect              # binary search history (e.g. for regressions)
    .gitignore              # specify intentionally untracked files to ignore
```
