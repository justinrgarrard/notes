---
layout: page
---

# CH 2 | Git Basics

### Create a Git Repository

**Option 01: Clone Down an Existing Repostiory**

1. `git clone https://<some_git_repository_url>`

**Option 02: Transform a Normal Directory into a Repository**

1. `git init`
2. `git add --all`
3. `git commit -m "Initial commit"`


### Track Changes on a Git Repository

* Use `git add <file>` to track any changes made to a file
* Use `git rm <file>` to stop tracking a file (and delete it)
* Use `git status` to check repository state
* Use `git commit -m "<commit_message>` to save the repository state as a snapshot
* Use `git dff` to view differences between the repository and its last snapshot
* Place filenames you want to ignore in a file named `.gitignore` to avoid commiting them

*Weird Behavior:* Git doesn't track file names very well, so use `git mv <old_filename> <new_filename>` to make a change.


### Viewing History

* Use `git log` to view previous commits

```bash
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number
```

* Specify additional flags to get exactly the output you're looking for

```bash
$ git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/

5610e3b - Fix testcase failure when extended attributes are in use
acd3b9e - Enhance hold_lock_file_for_{update,append}() API
f563754 - demonstrate breakage of detached checkout with symbolic link HEAD
d1a43f2 - reset --hard/read-tree --reset -u: remove unmerged new paths
51a94af - Fix "checkout --track -b newbranch" on detached HEAD
b0ad11e - pull: allow "git pull origin $something:$current_branch" into an unborn branch
```

### Undoing Things

* Use `git commit --amend` to redo a commit without creating another commit (i.e. add files you forgot)

* Use `git reset` to unstage a file prior to committing

```bash
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M	CONTRIBUTING.md
```

* Use `git checkout -- <filename>` to return a file to its unmodified state

```bash
$ git checkout -- CONTRIBUTING.md
```

### Working with Remotes

> "Remote repositories are versions of your project that are hosted on the Internet or network somewhere."

* List remotes with `git remote`

```bash
$ git remote -v
bakkdoor  https://github.com/bakkdoor/grit (fetch)
bakkdoor  https://github.com/bakkdoor/grit (push)
cho45     https://github.com/cho45/grit (fetch)
cho45     https://github.com/cho45/grit (push)
defunkt   https://github.com/defunkt/grit (fetch)
defunkt   https://github.com/defunkt/grit (push)
koke      git://github.com/koke/grit.git (fetch)
koke      git://github.com/koke/grit.git (push)
origin    git@github.com:mojombo/grit.git (fetch)
origin    git@github.com:mojombo/grit.git (push)
```

* Add remotes with `git remote add <shortname> <url>`

* Push to remotes with `git push <remote> <branch>`

* Get details about a remote using `git remote show origin`

```
$ git remote show origin
* remote origin
  URL: https://github.com/my-org/complex-project
  Fetch URL: https://github.com/my-org/complex-project
  Push  URL: https://github.com/my-org/complex-project
  HEAD branch: master
  Remote branches:
    master                           tracked
    dev-branch                       tracked
    markdown-strip                   tracked
    issue-43                         new (next fetch will store in remotes/origin)
    issue-45                         new (next fetch will store in remotes/origin)
    refs/remotes/origin/issue-11     stale (use 'git remote prune' to remove)
  Local branches configured for 'git pull':
    dev-branch merges with remote dev-branch
    master     merges with remote master
  Local refs configured for 'git push':
    dev-branch                     pushes to dev-branch                     (up to date)
    markdown-strip                 pushes to markdown-strip                 (up to date)
    master                         pushes to master                         (up to date)
```

* Change a remote's shortname using `git remote rename <old_shortname> <new_shortname>`

* Remove a remote with `git remote remove <shortname>`

### Tagging

* Tags come in two flavors: annotated and lightweight (general recommendation is to always use annotated)

* List tags with `git tag`

* Create an annotated tag on the current commit with `$ git tag -a <tag_name> -m "<tag description"`

* View tag information (and associated commits) with `git show <tag_name>`

```
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number
```

* Tag previous commits by specifying part of their hash; for example `git tag -a v1.4 ca82a6`

* Push tags like any other git object; `git push origin --tags`

* Delete tags with `git tag -d <tag_name>`

### Git Aliases

* You can specify aliases specific to git without using Bash, if you so choose

```
$ git config --global alias.last 'log -1 HEAD'

$ git last

commit 66938dae3329c7aebe598c2246a8e6af90d04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

    Test for current head

    Signed-off-by: Scott Chacon <schacon@example.com>
```

