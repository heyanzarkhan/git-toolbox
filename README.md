<div align="center">

# 🧰 git-toolbox

**The Git Command Cheat Sheet — from your first commit to interactive rebases.**

A clean, organized, **copy-paste-ready** reference for every Git command you'll actually use.
Built for beginners learning the ropes *and* pros who just need a quick reminder mid-merge-conflict.

<br/>

[![Stars](https://img.shields.io/github/stars/heyanzarkhan/git-toolbox?style=for-the-badge&logo=github&color=f9c513)](https://github.com/heyanzarkhan/git-toolbox/stargazers)
[![Forks](https://img.shields.io/github/forks/heyanzarkhan/git-toolbox?style=for-the-badge&logo=github&color=8957e5)](https://github.com/heyanzarkhan/git-toolbox/network/members)
[![License: MIT](https://img.shields.io/github/license/heyanzarkhan/git-toolbox?style=for-the-badge&color=0969da)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-2ea44f?style=for-the-badge)](CONTRIBUTING.md)

[⭐ Star this repo](https://github.com/heyanzarkhan/git-toolbox) &nbsp;·&nbsp; [🐛 Report a bug](https://github.com/heyanzarkhan/git-toolbox/issues/new?template=bug_report.md) &nbsp;·&nbsp; [✨ Request a command](https://github.com/heyanzarkhan/git-toolbox/issues/new?template=feature_request.md)

</div>

---

## 📖 Why git-toolbox?

- 🎯 **Everything in one place** — stop digging through 10 browser tabs while a rebase is half-finished.
- 📋 **Copy-paste ready** — real examples next to every command, not abstract `<placeholders>`.
- 🧠 **Beginner-friendly, pro-approved** — starts with the daily essentials, scales up to rebases, cherry-picks, and submodules.
- ⚡ **Zero fluff** — scannable tables you can `Ctrl / Cmd + F` in seconds.
- 🆓 **Free & open source** — MIT licensed. Fork it, print it, pin it to your second monitor.

> 💡 **New to Git?** Start with [Everyday Essentials](#everyday-essentials). &nbsp; **Already fluent?** Jump to [Changing Commits](#changing-commits).

---

## 📑 Table of Contents

- [Everyday Essentials](#everyday-essentials)
- [Configuration](#configuration)
- [Branches](#branches)
- [Pulling](#pulling)
- [Staged Changes](#staged-changes)
- [Changing Commits](#changing-commits)
- [Compare](#compare)
- [View](#view)
- [Stash](#stash)
- [Tags](#tags)
- [Remote](#remote)
- [Submodules](#submodules)
- [Best Practices](#best-practices)
- [Contributing](#contributing)

---

## Everyday Essentials

> The commands you'll reach for every single day.

| Command | Description | Example |
| --- | --- | --- |
| `git init` | Start a new Git repository in the current folder. | `git init` |
| `git clone <url>` | Copy a remote repository to your machine. | `git clone https://github.com/heyanzarkhan/git-toolbox.git` |
| `git status` | See staged, unstaged, and untracked changes. | `git status -s` *(short view)* |
| `git add <file>` | Stage a file (or `.` for everything) for the next commit. | `git add .` |
| `git commit -m "msg"` | Save staged changes with a message. | `git commit -m "Add login page"` |
| `git push` | Upload your local commits to the remote. | `git push origin main` |
| `git pull` | Fetch and merge the latest remote changes. | `git pull` |
| `git log --oneline` | View a compact, one-line-per-commit history. | `git log --oneline -10` |

---

## Configuration

| Command | Description | Example |
| --- | --- | --- |
| `git config --global user.name "foo"` | Sets the global username. | `git config --global user.name "John Doe"` |
| `git config --global user.email "foo@example.com"` | Sets the global email. | `git config --global user.email "john@example.com"` |
| `git config --list` | Displays the list of global configurations. | `git config --list` |

---

## Branches

| Command | Description |
| --- | --- |
| `git branch foo` | Create a new branch named `foo`. Example: `git branch feature-login` |
| `git branch -d foo` | Delete a branch named `foo`. Example: `git branch -d feature-login` |
| `git switch foo` | Switch to the branch `foo`. Example: `git switch main` |
| `git switch -c\|--create foo` | Create and switch to a new branch `foo`. Example: `git switch -c feature-search` |
| `git restore foo.js` | Undo all changes to the file `foo.js` in the working directory. |
| `git checkout foo.js` | Undo all changes to the file `foo.js` *(legacy; prefer `git restore`)*. |
| `git checkout foo` | Switch to branch `foo` *(legacy; prefer `git switch`)*. |
| `git checkout -b foo` | Create and switch to branch `foo` *(legacy; prefer `git switch -c`)*. |
| `git merge foo` | Merge branch `foo` into the current branch. Example: `git merge feature-update` |

---

## Pulling

| Command | Description |
| --- | --- |
| `git pull --rebase --prune` | Pull the latest changes, rebase local changes on top, and remove branches that no longer exist remotely. |

---

## Staged Changes

| Command | Description |
| --- | --- |
| `git add file.txt` | Stage a file named `file.txt` for commit. Example: `git add index.html` |
| `git add -p\|--patch file.txt` | Stage parts of a file's changes interactively. Example: `git add -p app.js` |
| `git mv file1.txt file2.txt` | Rename or move a file. Example: `git mv old-name.txt new-name.txt` |
| `git rm --cached file.txt` | Remove a file from staging without deleting it from disk. Example: `git rm --cached debug.log` |
| `git rm --force file.txt` | Unstage and delete a file from the working directory. Example: `git rm --force unused.js` |
| `git reset HEAD` | Unstage all changes but keep them in the working directory. |
| `git reset --hard HEAD` | Unstage and delete all changes. ⚠️ **Use with caution — this cannot be undone.** |
| `git clean -f\|--force -d` | Recursively remove untracked files and directories. Example: `git clean -fd` |
| `git clean -f\|--force -d -x` | Recursively remove untracked **and** ignored files. Example: `git clean -fdx` |

---

## Changing Commits

| Command | Description |
| --- | --- |
| `git reset 5720fdf` | Reset the current branch to a specific commit without modifying the working directory. |
| `git reset HEAD~1` | Reset to the previous commit while keeping changes in the working directory. |
| `git reset --hard 5720fdf` | Reset the branch **and** working directory to a commit. ⚠️ **Erases all uncommitted changes.** |
| `git commit --amend -m "New message"` | Modify the last commit message. Example: `git commit --amend -m "Fix typo in docs"` |
| `git commit --fixup 5720fdf` | Create a commit to fix or amend the specified commit. |
| `git revert 5720fdf` | Create a new commit that undoes a specific commit. |
| `git rebase --interactive origin/main` | Interactively rebase the current branch on top of `main`. |
| `git rebase --interactive 5720fdf` | Rebase to a specific commit interactively. |
| `git rebase --continue` | Continue the rebase after resolving conflicts. |
| `git rebase --abort` | Abort an ongoing rebase operation. |
| `git cherry-pick 5720fdf` | Copy a specific commit onto the current branch. |

---

## Compare

| Command | Description |
| --- | --- |
| `git diff` | Show changes between the working directory and the index. |
| `git diff HEAD HEAD~2` | Compare the current commit with two commits back. |
| `git diff main other` | Show changes between two branches. |

---

## View

| Command | Description |
| --- | --- |
| `git log` | View the commit history. Tip: `git log --oneline` for a concise view. |
| `git log --patch` | View commits along with their changes. |
| `git log --decorate --graph --oneline` | Visualize the commit history as a graph. |
| `git show HEAD` | Display details of the current commit. |
| `git blame file.txt` | See who made each change to a file, line by line. |

---

## Stash

| Command | Description |
| --- | --- |
| `git stash push -m "Message"` | Save uncommitted changes to the stash with a message. |
| `git stash --include-untracked` | Stash all uncommitted **and** untracked files. |
| `git stash list` | View all stashed changes. |
| `git stash apply` | Apply the most recent stash to the working directory. |
| `git stash clear` | Delete all stashes. |

---

## Tags

| Command | Description |
| --- | --- |
| `git tag` | List all tags. |
| `git tag -a\|--annotate 0.0.1 -m\|--message "Message"` | Create an annotated tag. Example: `git tag -a v1.0 -m "Initial release"` |
| `git push --tags` | Push tags to a remote repository. |

---

## Remote

| Command | Description |
| --- | --- |
| `git remote -v` | View the URLs of remote repositories. |
| `git remote add upstream <url>` | Add a new remote repository named `upstream`. |
| `git push --force-with-lease` | Force-push safely, ensuring no conflicting remote updates are overwritten. |
| `git push --tags` | Push all tags to the remote repository. |

---

## Submodules

| Command | Description |
| --- | --- |
| `git submodule status` | Check the status of all submodules. |

**Submodule workflow:**

1. Sync &nbsp;→&nbsp; `git submodule sync`
2. Initialize &nbsp;→&nbsp; `git submodule init`
3. Update &nbsp;→&nbsp; `git submodule update`

---

## Best Practices

- ✅ **Commit early, commit often** — small, frequent commits are easier to review and revert.
- ⚠️ **Rebase with care** — never rewrite history that's already been pushed and shared.
- 📦 **Stash is temporary** — great for context-switching, but not a backup strategy.
- 🛑 **Think twice before `--hard` and `-fdx`** — `git reset --hard` and `git clean -fdx` are irreversible.
- 🔐 **Prefer `--force-with-lease` over `--force`** — it refuses to clobber others' work.

---

## Contributing

Contributions are what make the open-source community amazing! 💛 Got a command, flag, or workflow that belongs here?

1. **Fork** the repo
2. **Create** your branch &nbsp;→&nbsp; `git switch -c add-awesome-command`
3. **Commit** your changes &nbsp;→&nbsp; `git commit -m "Add awesome command"`
4. **Push** and open a **Pull Request**

See [CONTRIBUTING.md](CONTRIBUTING.md) and the [Code of Conduct](CODE_OF_CONDUCT.md) for details.

---

<div align="center">

### ⭐ Found this useful?

If git-toolbox saved you a Google search, **drop it a star** — it genuinely helps other developers find it too.

<br/>

**Made with ❤️ by [Anzar Khan](https://github.com/heyanzarkhan)** &nbsp;·&nbsp; [oneit.live](https://oneit.live)

📄 Licensed under the [MIT License](LICENSE)

</div>
