# 1 · What is Git?

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; **Part 1: Foundations** &nbsp;·&nbsp; Next: [Installation &amp; Setup ➡️](02-installation-and-setup.md)

---

## The one-sentence answer

**Git is a *distributed version control system* — a tool that records snapshots of your project over time, so you can review history, undo mistakes, and collaborate with others without overwriting each other's work.**

If you've ever saved files named `report-final.docx`, `report-final-v2.docx`, `report-final-REALLY-final.docx` — congratulations, you've manually done what Git automates, except Git does it infinitely better.

---

## What problem does version control solve?

Imagine building software with a team:

- 👥 Five people editing the same files. Whose change wins?
- 🐛 A bug appears. *Which* change introduced it, and when?
- 🧪 You want to try a risky idea without breaking the working version.
- ⏪ You shipped something broken and need to roll back to last week.

A **Version Control System (VCS)** solves all of these. It tracks *every* change to *every* file, who made it, when, and why — and lets you move freely through that timeline.

---

## Centralized vs. Distributed

There are two families of version control:

### Centralized (CVCS) — e.g. SVN, CVS, Perforce
There is **one central server** that holds the project history. Everyone checks out files from it and commits back to it.

```
        ┌──────────────┐
        │  Central     │
        │  Server      │  ← single source of truth
        └──────┬───────┘
        ┌──────┼───────┐
     [Dev A] [Dev B] [Dev C]   ← only have a working copy
```

**Problem:** if the server goes down, nobody can commit or see history. If it's lost without backups, the *entire project history* is gone.

### Distributed (DVCS) — e.g. Git, Mercurial
**Every developer has a full copy of the entire repository** — all of the history, on their own machine.

```
   [Dev A: full repo] ⇄ [Remote: full repo] ⇄ [Dev B: full repo]
                              ⇅
                        [Dev C: full repo]
```

**Benefits:**
- ⚡ Almost everything is **local** → blazing fast (no network needed to commit, view history, or branch).
- 🛟 Every clone is a **complete backup**.
- 🌿 Branching and merging are cheap and safe, which encourages experimentation.

Git is the most popular DVCS by a massive margin.

---

## A short history of Git 📜

Git was created in **2005** by **Linus Torvalds** — the same person who created the **Linux kernel**.

Here's the story:

- The Linux kernel project (thousands of contributors worldwide) had been using a proprietary DVCS called **BitKeeper**, offered to them for free.
- In 2005, that free arrangement **broke down** and BitKeeper's license was revoked for the kernel community.
- Linus couldn't find an existing tool that met the kernel's needs, so — famously — he **wrote his own in about two weeks.**

He designed Git around a few firm goals:

| Goal | Why it mattered |
| --- | --- |
| ⚡ **Speed** | The kernel has a huge history; operations had to be instant. |
| 🌳 **Strong support for non-linear development** | Thousands of parallel branches needed to merge cleanly. |
| 🌐 **Fully distributed** | No reliance on a central server. |
| 🔒 **Data integrity** | History must be tamper-evident and impossible to silently corrupt. |

> 🧠 **Fun fact:** "git" is British slang for an unpleasant person. Linus joked: *"I'm an egotistical bastard, and I name all my projects after myself. First Linux, now git."*

In 2008, **GitHub** launched — a website that hosts Git repositories and adds collaboration features on top. It's a huge reason Git became the global standard. (More on the Git-vs-GitHub difference below.)

---

## How Git thinks about your data 🧩

This is the single most important mental model, and it's where Git differs from older tools.

Most older VCSs store data as a **list of file-based changes (deltas)** — "in version 3, line 10 of `app.js` changed to…".

**Git doesn't do that.** Git thinks of your data as a **series of snapshots.** Every time you commit, Git essentially takes a **picture of what all your files look like at that moment** and stores a reference to that snapshot.

```
Commit 1        Commit 2        Commit 3
┌────────┐      ┌────────┐      ┌────────┐
│ A      │      │ A      │      │ A'     │   ← A changed
│ B      │ ───▶ │ B'     │ ───▶ │ B'     │   ← B unchanged (Git reuses it)
│ C      │      │ C      │      │ C      │
└────────┘      └────────┘      └────────┘
```

For efficiency, if a file **hasn't** changed, Git doesn't store it again — it just links to the previous identical version. But conceptually, **every commit is a full snapshot**, not a diff. This is why branching, switching, and merging in Git are so fast and reliable.

---

## Git ≠ GitHub 🐙

A very common beginner confusion. They are **not** the same thing:

| | **Git** | **GitHub** |
| --- | --- | --- |
| **What it is** | A command-line *tool* | A *website / cloud service* |
| **Runs** | On your computer | In the browser / cloud |
| **Made by** | Linus Torvalds (open source) | A company (now owned by Microsoft) |
| **Needs internet?** | No | Yes |
| **Does** | Tracks versions of your code | *Hosts* your Git repos + adds pull requests, issues, CI, etc. |

**Analogy:** Git is like the *camera* that takes snapshots of your project. GitHub is like *Instagram* — a place to store those snapshots online and share/collaborate around them. Alternatives to GitHub include **GitLab** and **Bitbucket** — they all host Git repositories.

You can use Git with **no internet and no GitHub at all.** GitHub just makes collaborating dramatically easier.

---

## The big picture: Git's three areas

You'll meet these constantly. We cover them in depth in [Core Concepts](03-core-concepts.md), but here's the preview:

```
 Working Directory  →   Staging Area   →   Repository
   (your files)         (git add)          (git commit)
   "I'm editing"        "ready to save"    "saved forever"
```

1. **Working Directory** — the actual files you see and edit.
2. **Staging Area (Index)** — a "draft" of your next commit; you choose exactly what goes in.
3. **Repository (.git)** — where committed snapshots live permanently.

---

## ✅ Key takeaways

- Git is a **distributed** version control system — everyone has the full history locally.
- It was created by **Linus Torvalds in 2005** for the Linux kernel.
- Git stores **snapshots**, not differences — that's why it's fast and safe.
- **Git** is the tool on your machine; **GitHub** is a website that hosts Git repos.
- Work flows through three areas: **Working Directory → Staging Area → Repository.**

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; Next: [2 · Installation &amp; Setup ➡️](02-installation-and-setup.md)
