# 10 · Command Reference

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Advanced Git](09-advanced-git.md) &nbsp;·&nbsp; Next: [GitHub Essentials ➡️](11-github-essentials.md)

---

The encyclopedic list — every command you're likely to need, grouped by task, with a one-line description and example. For a printable one-pager, see the [Cheat Sheet](../CHEATSHEET.md). For *explanations*, follow the chapter links in each section.

**Jump to:** [Setup](#setup--config) · [Create](#create--clone) · [Snapshot](#snapshotting) · [Inspect](#inspecting) · [Branches](#branching) · [Merge/Rebase](#merging--rebasing) · [Remotes](#remotes) · [Undo](#undoing) · [Stash](#stashing) · [Tags](#tags) · [Advanced](#advanced) · [Help](#help)

---

## Setup &amp; Config
> See [Chapter 2](02-installation-and-setup.md)

| Command | Description |
| --- | --- |
| `git config --global user.name "Name"` | Set your commit author name |
| `git config --global user.email "you@x.com"` | Set your commit author email |
| `git config --global init.defaultBranch main` | Default new repos to a `main` branch |
| `git config --global core.editor "code --wait"` | Set the default editor |
| `git config --global alias.co checkout` | Create a shortcut (`git co`) |
| `git config --list` | List all settings |
| `ssh-keygen -t ed25519 -C "you@x.com"` | Generate an SSH key for GitHub |

## Create &amp; Clone
> See [Chapter 4](04-everyday-git.md)

| Command | Description |
| --- | --- |
| `git init` | Start a new repo in the current folder |
| `git clone <url>` | Copy a remote repo (history + files) |
| `git clone <url> <dir>` | Clone into a specific folder |
| `git clone --depth 1 <url>` | Shallow clone (latest commit only — faster) |
| `git clone --recurse-submodules <url>` | Clone including submodules |

## Snapshotting
> See [Chapter 4](04-everyday-git.md)

| Command | Description |
| --- | --- |
| `git status` | Show staged / unstaged / untracked changes |
| `git status -s` | Short, compact status |
| `git add <file>` | Stage a file |
| `git add .` | Stage everything in the current dir |
| `git add -p` | Stage selected *parts* of files interactively |
| `git commit -m "msg"` | Commit staged changes |
| `git commit -am "msg"` | Stage tracked files **and** commit |
| `git commit --amend` | Modify the most recent commit |
| `git rm <file>` | Delete a file and stage the deletion |
| `git rm --cached <file>` | Stop tracking a file (keep it on disk) |
| `git mv <old> <new>` | Rename/move a file (staged) |

## Inspecting
> See [Chapter 4](04-everyday-git.md)

| Command | Description |
| --- | --- |
| `git log` | Commit history |
| `git log --oneline --graph --all` | Compact visual history of all branches |
| `git log -p` | History with the actual diffs |
| `git log --author="Name"` | Filter by author |
| `git log --since="2 weeks ago"` | Filter by date |
| `git show <hash>` | Show a commit's details &amp; changes |
| `git diff` | Unstaged changes |
| `git diff --staged` | Staged changes (next commit) |
| `git diff <a> <b>` | Compare two branches/commits |
| `git blame <file>` | Who last changed each line |
| `git grep "text"` | Search tracked files for a string |

## Branching
> See [Chapter 5](05-branching-and-merging.md)

| Command | Description |
| --- | --- |
| `git branch` | List local branches |
| `git branch -a` | List local **and** remote branches |
| `git branch <name>` | Create a branch |
| `git switch <name>` | Switch to a branch |
| `git switch -c <name>` | Create **and** switch |
| `git switch -` | Switch to the previous branch |
| `git checkout <name>` | Switch (legacy syntax) |
| `git branch -m <new>` | Rename current branch |
| `git branch -d <name>` | Delete a merged branch |
| `git branch -D <name>` | Force-delete a branch |
| `git branch -vv` | Show tracking info for each branch |

## Merging &amp; Rebasing
> See [Chapter 5](05-branching-and-merging.md) &amp; [Chapter 8](08-rewriting-history.md)

| Command | Description |
| --- | --- |
| `git merge <branch>` | Merge a branch into the current one |
| `git merge --no-ff <branch>` | Force a merge commit |
| `git merge --abort` | Cancel a conflicted merge |
| `git rebase <branch>` | Replay current branch onto another |
| `git rebase -i HEAD~<n>` | Interactively edit the last *n* commits |
| `git rebase --continue` / `--skip` / `--abort` | Control an in-progress rebase |
| `git cherry-pick <hash>` | Copy a single commit onto this branch |

## Remotes
> See [Chapter 6](06-working-with-remotes.md)

| Command | Description |
| --- | --- |
| `git remote -v` | List remotes and their URLs |
| `git remote add <name> <url>` | Add a remote |
| `git remote remove <name>` | Remove a remote |
| `git fetch <remote>` | Download remote changes (no merge) |
| `git pull` | Fetch **and** merge |
| `git pull --rebase` | Fetch, then rebase local commits on top |
| `git push` | Upload commits to the remote |
| `git push -u origin <branch>` | Push &amp; set upstream (first push) |
| `git push origin --delete <branch>` | Delete a remote branch |
| `git push --force-with-lease` | Safe force-push after a rewrite |

## Undoing
> See [Chapter 7](07-undoing-changes.md)

| Command | Description |
| --- | --- |
| `git restore <file>` | Discard unstaged changes to a file |
| `git restore --staged <file>` | Unstage a file (keep edits) |
| `git reset --soft HEAD~1` | Undo last commit, keep changes **staged** |
| `git reset --mixed HEAD~1` | Undo last commit, keep changes unstaged |
| `git reset --hard HEAD~1` | Undo last commit, **discard** changes ⚠️ |
| `git revert <hash>` | New commit that undoes an old one (safe) |
| `git reflog` | History of where HEAD has been (recovery) |
| `git clean -n` / `-fd` | Preview / delete untracked files |

## Stashing
> See [Chapter 9](09-advanced-git.md)

| Command | Description |
| --- | --- |
| `git stash` | Shelve tracked changes |
| `git stash -u` | Include untracked files |
| `git stash list` | List stashes |
| `git stash pop` | Re-apply &amp; remove the latest stash |
| `git stash apply` | Re-apply but keep the stash |
| `git stash drop` / `clear` | Delete one / all stashes |

## Tags
> See [Chapter 9](09-advanced-git.md)

| Command | Description |
| --- | --- |
| `git tag` | List tags |
| `git tag -a v1.0 -m "msg"` | Create an annotated tag |
| `git push origin v1.0` | Push a single tag |
| `git push --tags` | Push all tags |
| `git tag -d v1.0` | Delete a local tag |

## Advanced
> See [Chapter 9](09-advanced-git.md)

| Command | Description |
| --- | --- |
| `git bisect start` / `good` / `bad` | Binary-search for a bad commit |
| `git worktree add <path> <branch>` | Check out a branch in another folder |
| `git submodule update --init` | Initialize submodules |
| `git gc` | Garbage-collect &amp; compress the repo |
| `git fsck` | Check repository integrity |
| `git archive -o site.zip HEAD` | Export a snapshot to a zip |

## Help

| Command | Description |
| --- | --- |
| `git help <command>` | Full manual for a command |
| `git <command> -h` | Quick usage summary |
| `git <command> --help` | Open the full docs |

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Advanced Git](09-advanced-git.md) &nbsp;·&nbsp; Next: [11 · GitHub Essentials ➡️](11-github-essentials.md)
