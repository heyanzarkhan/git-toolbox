# 17 · Glossary

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Troubleshooting](16-troubleshooting.md)

---

Every term in this handbook, defined in one line. 📖

---

### A–C

- **Atomic commit** — A commit containing exactly one logical change.
- **Bare repository** — A repo with no working directory, used as a shared remote.
- **Bisect** — Binary-search through history to find the commit that introduced a bug.
- **Blob** — Git's internal object that stores a file's *contents* (not its name).
- **Branch** — A lightweight, movable pointer to a commit; an independent line of work.
- **CI/CD** — Continuous Integration / Continuous Deployment: automatically test and ship changes.
- **Checkout** — Switch branches or restore files (legacy command; see `switch`/`restore`).
- **Cherry-pick** — Copy a specific commit onto the current branch.
- **Clone** — Download a full copy of a remote repository.
- **Commit** — A saved snapshot of your project at a point in time.
- **Conflict** — When two branches change the same lines and Git needs you to choose.
- **CODEOWNERS** — A file defining who is auto-requested to review specific paths.

### D–G

- **Detached HEAD** — When `HEAD` points directly at a commit instead of a branch.
- **Diff** — The set of differences between two versions.
- **Distributed VCS** — A version control system where everyone has the full history (e.g. Git).
- **Fast-forward** — A merge where the branch pointer simply slides forward (no merge commit).
- **Fetch** — Download remote changes *without* merging them into your work.
- **Fork** — Your personal server-side copy of someone else's repository.
- **Git** — The distributed version control tool itself.
- **GitHub** — A cloud platform that hosts Git repos and adds collaboration features.
- **`.gitignore`** — A file listing paths Git should not track.

### H–O

- **HEAD** — A pointer to your current location (usually the tip of the current branch).
- **Hook** — A script Git runs automatically on events (e.g. `pre-commit`).
- **Index** — Another name for the **staging area**.
- **Issue** — A tracked unit of work: bug, feature, task, or question.
- **LFS (Large File Storage)** — A Git extension for versioning large binary files.
- **Main / Master** — The default primary branch name (`main` is the modern default).
- **Merge** — Combine the histories of two branches.
- **Merge commit** — A commit with two parents, created by a non-fast-forward merge.
- **Monorepo** — A single repository containing many projects/packages.
- **Origin** — The default nickname for the remote you cloned from.

### P–R

- **Pull** — `fetch` + `merge`: download remote changes and integrate them.
- **Pull Request (PR)** — A proposal to merge one branch into another, with review.
- **Push** — Upload your local commits to a remote.
- **Rebase** — Replay commits onto a new base for a linear history.
- **Reflog** — A log of everywhere `HEAD` has been; your recovery safety net.
- **Remote** — A hosted version of your repo (e.g. on GitHub).
- **Remote-tracking branch** — A local cache of a remote branch's state (e.g. `origin/main`).
- **Repository (repo)** — A project tracked by Git (the `.git` database + your files).
- **Revert** — Create a *new* commit that undoes a previous one (safe for shared history).

### S–Z

- **SHA / hash** — The unique 40-character ID of a Git object (commit, blob, etc.).
- **Snapshot** — Git's model of your project at a commit (vs. storing diffs).
- **Squash** — Combine multiple commits into one.
- **Staging area** — The "draft" of your next commit; you choose what `git add` puts here.
- **Stash** — Temporarily shelve uncommitted changes.
- **Submodule** — A Git repository nested inside another at a pinned commit.
- **Tag** — A named pointer to a specific commit, usually marking a release.
- **Tracking branch** — A local branch linked to a remote (upstream) branch.
- **Trunk-Based Development** — A workflow where everyone integrates into `main` frequently.
- **Untracked file** — A file in your working directory that Git isn't yet tracking.
- **Upstream** — The remote branch your local branch is linked to; also the original repo of a fork.
- **Working directory (working tree)** — The actual files on disk that you edit.
- **Worktree** — An additional checked-out working directory linked to the same repo.

---

> 🎉 **You've reached the end of the handbook!** Loop back to the [Home page](../README.md), grab the [Cheat Sheet](../CHEATSHEET.md), or — if this helped Git finally click — **[give the repo a ⭐](https://github.com/heyanzarkhan/git-toolbox)**.

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Troubleshooting](16-troubleshooting.md)
