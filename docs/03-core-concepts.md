# 3 · Core Concepts

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Installation &amp; Setup](02-installation-and-setup.md) &nbsp;·&nbsp; Next: [Everyday Git ➡️](04-everyday-git.md)

---

This is the most important chapter in the handbook. Once these ideas click, every Git command starts to make sense. Read it slowly. ☕

---

## The repository (`.git`)

A **repository** ("repo") is a project folder that Git is tracking. When you run `git init`, Git creates a hidden subfolder called **`.git`** inside it:

```
my-project/
├── .git/          ← the repository database (history, branches, config)
├── index.html
└── style.css
```

That `.git` folder **is** the repository — it holds every snapshot, branch, and setting. Delete it, and your folder becomes a normal folder again (your current files stay, but the history is gone). Everything else (`index.html`, `style.css`) is your **working directory**.

---

## The three areas 🗂️

Git work flows through **three areas**. Internalize this diagram:

```
   Working Directory        Staging Area (Index)        Repository
   ─────────────────        ────────────────────        ──────────
   Files you edit    ──┐    A curated draft of      ──┐  Permanent
                       │    your next commit          │  snapshots
        git add  ──────┘         git commit  ─────────┘  (history)
```

| Area | What it is | You put things here with |
| --- | --- | --- |
| **Working Directory** | The real files on disk you're editing | (just editing files) |
| **Staging Area** (aka *Index*) | A drafting space — you choose *exactly* what goes into the next commit | `git add` |
| **Repository** | The committed history, stored in `.git` | `git commit` |

> 💡 **Why a staging area?** It lets you craft clean commits. You might change 5 files but only want to commit 2 of them together as one logical change. Staging gives you that control.

---

## The three states of a file

Every tracked file is in one of these states at any moment:

```
   modified  ──(git add)──▶  staged  ──(git commit)──▶  committed
   "changed but            "marked for             "safely saved
    not marked"             next commit"            in history"
```

- **Modified** — you changed the file, but haven't staged it yet.
- **Staged** — you've marked the modified file to go into your next commit.
- **Committed** — the data is safely stored in your local repository.

A brand-new file Git has never seen is **untracked** — Git ignores it until you `git add` it.

You inspect all of this with the command you'll run more than any other:

```bash
git status
```

---

## Commits &amp; the SHA hash 🔑

A **commit** is a single saved snapshot. Each commit records:

- A snapshot of all your files at that moment
- The **author** and **committer** (name, email, timestamp)
- A **message** describing the change
- A pointer to its **parent** commit(s) — forming a chain

Every commit gets a unique **40-character SHA-1 hash** as its ID:

```
commit 9c6c1f4a2b7e... (HEAD -> main)
Author:  Anzar Khan <you@example.com>
Date:    Mon May 31 09:00 2026
    Add login form
```

You usually only need the **first 7 characters** (`9c6c1f4`) to refer to a commit. This hash is calculated from the commit's *contents*, which is how Git guarantees **integrity** — if even one byte changed, the hash would change.

Commits link backward to their parents, forming the project's history:

```
  A ◀── B ◀── C ◀── D        (each arrow = "my parent is…")
                    ▲
                  HEAD
```

---

## HEAD, branches &amp; refs 🌿

These three are tightly related — and beginners mix them up constantly. Let's untangle them.

### A branch is just a pointer
A **branch** in Git is *not* a heavy copy of your files. It's simply a **lightweight, movable pointer to a commit.** That's it. Creating a branch just writes a new pointer — which is why it's instant.

```
              main
                │
                ▼
  A ◀── B ◀── C
```

When you commit on `main`, the `main` pointer moves forward to the new commit:

```
                     main
                       │
                       ▼
  A ◀── B ◀── C ◀── D
```

### HEAD = "where am I right now?"
**`HEAD`** is a special pointer that tells you **which branch (or commit) you're currently on.** Usually `HEAD` points at a branch, and that branch points at a commit:

```
  HEAD → main → D
```

When you `git switch feature`, all that happens is `HEAD` now points to `feature`. Switching branches is just moving this pointer (and updating your working files to match) — no copying, no slow operations.

### Refs
A **ref** is just a named pointer to a commit. Branches, tags, and `HEAD` are all refs under the hood, stored in `.git/refs`.

---

## How Git stores data (a peek under the hood) 🔬

Optional, but it demystifies everything. Git's database stores four object types, each identified by its SHA hash:

| Object | Stores |
| --- | --- |
| 🟦 **blob** | The *contents* of a file (no name, just data) |
| 🟩 **tree** | A directory listing: filenames + which blob/tree each points to |
| 🟨 **commit** | A snapshot: points to one tree + parent commit(s) + author + message |
| 🏷️ **tag** | A named, annotated pointer to a specific commit |

So a commit points to a tree (your folder), which points to blobs (your files):

```
commit ──▶ tree ──▶ blob (index.html)
                └──▶ blob (style.css)
```

Because identical content always produces the same hash, Git **never stores the same file twice** — even across thousands of commits. Elegant. ✨

---

## Putting it together: the lifecycle of a change

```
1. Edit index.html              → file is now "modified"
2. git add index.html           → file is now "staged"
3. git commit -m "Update title" → snapshot saved; branch pointer moves; HEAD follows
4. git push                     → your commits are uploaded to the remote (e.g. GitHub)
```

You now know what each of those steps actually *does*. The next chapter puts it into practice.

---

## ✅ Key takeaways

- The **`.git` folder** is the repository; everything else is your **working directory**.
- Changes flow through **three areas**: Working Directory → **Staging** (`git add`) → **Repository** (`git commit`).
- A file is **untracked, modified, staged, or committed** — `git status` shows which.
- A **commit** is a snapshot with a unique **SHA hash**, linked to its parent(s).
- A **branch is just a movable pointer** to a commit; **HEAD** marks where you are now.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Installation &amp; Setup](02-installation-and-setup.md) &nbsp;·&nbsp; Next: [4 · Everyday Git ➡️](04-everyday-git.md)
