# 4 · Everyday Git

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Core Concepts](03-core-concepts.md) &nbsp;·&nbsp; Next: [Branching &amp; Merging ➡️](05-branching-and-merging.md)

---

This is the daily-driver chapter — the 90% of Git you'll use every single day. We'll create a repository from scratch and walk a change all the way from your editor to GitHub.

---

## Starting a repository

You start a repo one of two ways:

### Option A — brand-new project: `git init`
```bash
mkdir my-project && cd my-project
git init                 # creates the hidden .git folder
# → Initialized empty Git repository in .../my-project/.git/
```

### Option B — existing project on GitHub: `git clone`
```bash
git clone https://github.com/heyanzarkhan/git-toolbox.git
cd git-toolbox
```
`clone` downloads the **entire history**, not just the latest files, and automatically sets up a remote called `origin` pointing back to where you cloned from.

---

## The core loop: status → add → commit

This three-step rhythm is the heartbeat of Git.

### 1. See what's going on: `git status`
```bash
git status
# Shows: untracked files, modified files, and what's staged
git status -s            # short, compact format
```

### 2. Stage changes: `git add`
```bash
git add index.html           # stage one file
git add src/ docs/           # stage folders
git add .                    # stage everything in the current directory
git add -p                   # interactively stage *parts* of files (powerful!)
```

> 💡 `git add -p` (patch mode) lets you review and stage change-by-change — perfect for splitting unrelated edits into separate, clean commits.

### 3. Save a snapshot: `git commit`
```bash
git commit -m "Add login form"

# Stage all *tracked* modified files AND commit in one step:
git commit -am "Fix typo in header"

# Open your editor to write a longer, multi-line message:
git commit
```

**What makes a good commit message?**
```
Add password-reset email flow

- Send a tokenized reset link valid for 30 minutes
- Add rate limiting to prevent abuse
```
A short imperative summary line (≤ 50 chars), a blank line, then details. More on conventions in [Best Practices](15-best-practices-and-workflows.md).

---

## Ignoring files: `.gitignore`

Some files should **never** be committed — secrets, dependencies, build output, OS junk. Create a file named `.gitignore` in your repo root:

```gitignore
# Dependencies
node_modules/

# Environment / secrets
.env
*.key

# Build output
dist/
build/

# OS / editor noise
.DS_Store
.vscode/
```

> ⚠️ `.gitignore` only ignores **untracked** files. If a file is *already tracked*, ignoring it later won't help — you must first stop tracking it: `git rm --cached secret.env`.

---

## Viewing history: `git log`

```bash
git log                              # full history, newest first
git log --oneline                    # one compact line per commit
git log --oneline --graph --all      # visual graph of all branches
git log -p                           # show the actual changes (patches)
git log -5                           # only the last 5 commits
git log --author="Anzar"             # filter by author
git log --since="2 weeks ago"        # filter by date
git show 9c6c1f4                     # full details of one commit
```

A great alias to live by:
```bash
git config --global alias.lg "log --oneline --graph --decorate --all"
git lg
```

---

## Inspecting changes: `git diff`

```bash
git diff                 # unstaged changes (working dir vs staging)
git diff --staged        # staged changes (what will be committed)
git diff main feature    # difference between two branches
git diff HEAD~1 HEAD     # difference between the last two commits
```

---

## Sending &amp; receiving: `push` and `pull`

Once you have a remote (like GitHub):

```bash
git push                 # upload your commits to the remote
git push -u origin main  # first push: set 'main' to track origin/main
git pull                 # fetch remote changes AND merge them into your branch
```

> `git pull` = `git fetch` (download) + `git merge` (integrate). We unpack remotes fully in [Chapter 6](06-working-with-remotes.md).

---

## A complete first-project walkthrough 🚶

```bash
mkdir hello-git && cd hello-git
git init

echo "# Hello Git" > README.md
git status                     # README.md is untracked

git add README.md
git status                     # README.md is now staged

git commit -m "Add README"
git log --oneline              # your first commit! 🎉

# Connect to an empty GitHub repo you created:
git remote add origin git@github.com:you/hello-git.git
git branch -M main
git push -u origin main        # live on GitHub
```

---

## ✅ Key takeaways

- Start with `git init` (new) or `git clone` (existing).
- The daily loop is **`status` → `add` → `commit`**.
- Use `.gitignore` to keep secrets, dependencies, and junk out of history.
- `git log` (especially `--oneline --graph`) is your window into history.
- `git push` uploads; `git pull` downloads + merges.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Core Concepts](03-core-concepts.md) &nbsp;·&nbsp; Next: [5 · Branching &amp; Merging ➡️](05-branching-and-merging.md)
