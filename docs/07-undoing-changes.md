# 7 · Undoing Changes

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Working with Remotes](06-working-with-remotes.md) &nbsp;·&nbsp; Next: [Rewriting History ➡️](08-rewriting-history.md)

---

Everyone makes mistakes — Git's killer feature is that **almost nothing is permanent.** This chapter is your safety net. Bookmark it. 🔖

First, a quick map of "which command do I want?":

| I want to… | Use |
| --- | --- |
| Discard edits to a file (not yet committed) | `git restore <file>` |
| Unstage a file (keep the edits) | `git restore --staged <file>` |
| Fix the **last** commit's message or contents | `git commit --amend` |
| Move the branch pointer back, keep/discard changes | `git reset` |
| Undo a commit **safely** (on shared history) | `git revert` |
| Recover something I think I lost | `git reflog` |
| Delete untracked files | `git clean` |

---

## Discarding uncommitted changes: `git restore`

```bash
git restore index.html         # throw away unstaged edits to a file ⚠️ irreversible
git restore .                  # discard ALL unstaged changes
git restore --staged index.html   # unstage (move from staged → modified), keep edits
git restore --source=HEAD~2 app.js # restore a file as it was 2 commits ago
```

> ⚠️ `git restore <file>` permanently discards uncommitted work — there's no undo, because Git never saved it.

---

## `git reset` — moving the branch pointer

`reset` moves your current branch to point at a different commit. The `--soft / --mixed / --hard` flag decides **what happens to your changes:**

```bash
git reset --soft  HEAD~1    # undo last commit; KEEP changes STAGED
git reset --mixed HEAD~1    # undo last commit; keep changes UNSTAGED (default)
git reset --hard  HEAD~1    # undo last commit; DISCARD changes entirely ⚠️💀
```

Visualizing the three modes after `reset HEAD~1`:

| Flag | Branch pointer | Staging area | Working files |
| --- | --- | --- | --- |
| `--soft` | moves back | **kept** | **kept** |
| `--mixed` *(default)* | moves back | reset | **kept** |
| `--hard` | moves back | reset | **wiped** ⚠️ |

**Classic use — "I committed too early":**
```bash
git reset --soft HEAD~1     # uncommit, but my changes stay staged, ready to redo
```

**Classic use — "unstage everything":**
```bash
git reset                   # same as: git reset --mixed HEAD
```

> 💀 `git reset --hard` throws away uncommitted work. Be sure before you run it. (Even then — committed work can often be rescued via `reflog`, see below.)

---

## `git revert` — the safe undo

`reset` rewrites history, which is dangerous on **shared** branches. `revert` instead creates a **new commit that undoes** a previous one — leaving history intact. This is the **safe** way to undo something already pushed.

```bash
git revert 9c6c1f4          # make a new commit that reverses commit 9c6c1f4
git revert HEAD             # undo the most recent commit (safely)
git revert --no-commit HEAD~2..HEAD   # stage the reversal of a range, commit yourself
```

```
Before:  A ◀ B ◀ C(bug)
After:   A ◀ B ◀ C ◀ C'   ← C' undoes C; nothing was erased ✅
```

> 📌 **Rule of thumb:** `reset` for *local, unpushed* mistakes. `revert` for anything *already shared*.

---

## `git commit --amend` — fix the last commit

```bash
git commit --amend -m "Correct message"   # change the last commit's message
git add forgotten.js
git commit --amend --no-edit              # add a forgotten file to the last commit
```

> ⚠️ Amending **rewrites** the last commit (new hash). Only amend commits you haven't pushed — or you'll need a `--force-with-lease` push.

---

## `git reflog` — your time machine ⏳

This is the command that has saved countless developers from panic. The **reflog** records *every* place `HEAD` has been — even after resets, rebases, and "deleted" commits. As long as the commit existed recently, it's recoverable.

```bash
git reflog
# 9c6c1f4 HEAD@{0}: reset: moving to HEAD~1
# a1b2c3d HEAD@{1}: commit: The work I thought I lost!
```

Recover it:
```bash
git reset --hard a1b2c3d          # jump back to that exact state
# or, more safely, grab it onto a new branch:
git switch -c rescue a1b2c3d
```

> 🛟 **Did a `--hard reset` eat your commits?** Don't panic — run `git reflog`, find the hash, and restore it. Git keeps unreachable commits for ~30–90 days before garbage-collecting them.

---

## `git clean` — remove untracked files

`reset` and `restore` don't touch **untracked** files. `clean` does:

```bash
git clean -n               # DRY RUN — show what WOULD be deleted (always do this first!)
git clean -f               # delete untracked files
git clean -fd              # delete untracked files AND directories
git clean -fdx             # ...also delete ignored files (e.g. node_modules) ⚠️
```

> ⚠️ `git clean` is irreversible — those files were never in Git. **Always run `git clean -n` first.**

---

## 🆘 "Oh no" quick recovery guide

| Situation | Fix |
| --- | --- |
| Edited a file, want the committed version back | `git restore <file>` |
| `git add`ed something by mistake | `git restore --staged <file>` |
| Committed too early / wrong message | `git commit --amend` or `git reset --soft HEAD~1` |
| Need to undo a **pushed** commit | `git revert <hash>` |
| Ran `reset --hard`, lost commits | `git reflog` → `git reset --hard <hash>` |
| Wrong branch for your last commit | `git reset --soft HEAD~1`, switch branch, re-commit |

---

## ✅ Key takeaways

- `restore` = discard/unstage working changes; `reset` = move the branch pointer (`--soft`/`--mixed`/`--hard`).
- **`revert` is the safe undo** for shared history; **`reset` is for local** mistakes.
- `commit --amend` fixes the *last* commit only — don't amend pushed commits.
- **`git reflog` can rescue almost anything** you think you've lost.
- `git clean` deletes untracked files — always `-n` (dry run) first.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Working with Remotes](06-working-with-remotes.md) &nbsp;·&nbsp; Next: [8 · Rewriting History ➡️](08-rewriting-history.md)
