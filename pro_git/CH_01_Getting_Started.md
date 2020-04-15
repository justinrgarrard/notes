---
layout: page
---

# CH 1 | Getting Started

> "Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later."

![Git Model](../resources/git_model.png)

|                                     |                 |                                                                            |
| ----------------------------------- | --------------- | -------------------------------------------------------------------------- |
| Local Version Control Systems       | RCS             | Tracks changes for a single local system.                                  |
| Centralized Version Control Systems | Subversion, TFS | Tracks changes from a hub, accessed by clients.                            |
| Distributed Version Control Systems | Git, Mercurial  | Mirrors entire system across all clients, removing single point of failure |


### Snapshot Model

> "Instead, Git thinks of its data more like a series of snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot."

![Git Snapshots](../resources/git_snapshots.png)


### Git Qualities
* Git is local (everything is stored on your local system)
* Git is fast (because everything is local)
* Git is checksummed (all objects have hash references)
* Git only adds data (nothing is ever lost, only "patched" with an undo sticker)


### Three States

> "Git has three main states that your files can reside in: modified, staged, and committed:

    Modified means that you have changed the file but have not committed it to your database yet.

    Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

    Committed means that the data is safely stored in your local database.

![Git States](../resources/git_states.png)


### First Time Setup

* Use `git config` to set configurations
  * `git config --global user.name "John Doe"`
  * `git config --global user.email johndoe@example.com`
  * `git config --global core.editor vim`

* Data is stored in:
  * (System) /etc/gitconfig
  * (Global/User) ~/.gitconfig
  * (Project) .git/config

* List configurations with `git config --list`