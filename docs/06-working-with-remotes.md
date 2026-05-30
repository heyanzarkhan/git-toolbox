# 6 · Working with Remotes

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Branching &amp; Merging](05-branching-and-merging.md) &nbsp;·&nbsp; Next: [Undoing Changes ➡️](07-undoing-changes.md)

---

A **remote** is a version of your repository hosted somewhere else — usually on GitHub, GitLab, or Bitbucket. Remotes are how you back up your work and collaborate with others.

---

## What is `origin`?

When you `git clone` a repo, Git automatically creates a remote named **`origin`** pointing at the URL you cloned from. `origin` is just a **nickname** for that URL so you don't have to type it every time.

```bash
git remote -v
# origin  git@github.com:you/project.git (fetch)
# origin  git@github.com:you/project.git (push)
```

Managing remotes:
```bash
git remote add origin git@github.com:you/project.git   # add a remote
git remote add upstream git@github.com:original/project.git  # add a 2nd (for forks)
git remote rename origin gh                             # rename
git remote remove origin                               # remove
git remote show origin                                 # detailed info
```

> 🍴 When you **fork** someone's project, the convention is: `origin` = your fork, `upstream` = the original. You pull updates from `upstream` and push your work to `origin`.

---

## `fetch` vs `pull` — the crucial difference

This trips up almost everyone. Both download from the remote, but:

| | `git fetch` | `git pull` |
| --- | --- | --- |
| Downloads remote commits? | ✅ Yes | ✅ Yes |
| Changes your working files? | ❌ **No** | ✅ Yes (merges them in) |
| Safe to run anytime? | ✅ Always safe | ⚠️ Can cause conflicts |

```bash
git fetch origin        # download everything, but DON'T touch my files
# ...now inspect what changed...
git log HEAD..origin/main --oneline   # see what's new on the remote
git merge origin/main   # integrate it when you're ready
```

**`git pull` is literally `git fetch` + `git merge`** in one command. Use `fetch` when you want to *look before you leap*; use `pull` when you just want the latest.

```bash
git pull                       # fetch + merge
git pull --rebase              # fetch, then REBASE your local commits on top (linear history)
git pull --rebase --prune      # ...and delete refs for branches deleted on the remote
```

> 💡 Many teams prefer `git pull --rebase` to avoid noisy "Merge branch 'main'" commits. You can make it the default: `git config --global pull.rebase true`.

---

## Pushing your work

```bash
git push                       # push current branch to its tracked remote branch
git push -u origin feature-x   # first push of a new branch: set up tracking
git push origin --delete old-branch   # delete a branch on the remote
git push --tags                # push your tags too
```

The `-u` (`--set-upstream`) flag links your local branch to a remote branch, so future `git push` / `git pull` need no arguments.

### Force-pushing safely
After rewriting history (e.g. a rebase), a normal push is rejected. **Never use plain `--force` on shared branches** — it can erase teammates' work. Use the safe version:
```bash
git push --force-with-lease    # ✅ refuses if someone else pushed in the meantime
git push --force               # ⚠️ dangerous: overwrites remote unconditionally
```

---

## Tracking branches

A **tracking branch** is a local branch linked to a remote branch (its *upstream*). This is what lets `git status` say *"Your branch is ahead of 'origin/main' by 2 commits."*

```bash
git branch -vv                         # show which remote each local branch tracks
git switch feature                     # auto-creates a tracking branch if origin/feature exists
git branch -u origin/main              # set upstream for the current branch
```

`origin/main` (with a slash) is a **remote-tracking branch** — your local cached snapshot of where `main` was on the remote *the last time you fetched*. It only updates when you `fetch`/`pull`.

---

## Typical collaboration flow

```bash
git switch main
git pull                       # 1. get the latest before starting
git switch -c fix-navbar       # 2. branch for your task
# ...work, add, commit...
git push -u origin fix-navbar  # 3. publish your branch
# 4. open a Pull Request on GitHub (see Chapter 12)
```

---

## ✅ Key takeaways

- A **remote** is a hosted copy of your repo; **`origin`** is the default nickname for it.
- `git fetch` downloads **without** changing your files; `git pull` = `fetch` + `merge`.
- `origin/main` is a *cached* pointer to the remote, updated only on fetch/pull.
- Use `git push -u origin branch` on a branch's first push.
- Prefer `--force-with-lease` over `--force` — never blow away shared history.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Branching &amp; Merging](05-branching-and-merging.md) &nbsp;·&nbsp; Next: [7 · Undoing Changes ➡️](07-undoing-changes.md)
