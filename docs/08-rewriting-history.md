# 8 · Rewriting History

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Undoing Changes](07-undoing-changes.md) &nbsp;·&nbsp; Next: [Advanced Git ➡️](09-advanced-git.md)

---

Sometimes you want to *reshape* history rather than just undo it — to clean up messy commits before sharing, or to keep history tidy and linear. That's what `rebase` and friends are for. These are power tools: sharp, useful, and worth respecting.

---

## ⚖️ The Golden Rule of Rebasing

> ### **Never rewrite history that other people have already pulled.**

Rebasing **changes commit hashes**. If you rewrite commits that teammates already have, your histories diverge and you'll create a painful mess. So:

- ✅ Rewrite freely on your **own local, unpushed** branch.
- ❌ Don't rebase `main` or any shared branch others are building on.

Keep that in mind and rebasing is safe and wonderful.

---

## `git rebase` — replay commits onto a new base

A **merge** ties two branches together with a merge commit. A **rebase** instead *moves* your branch's commits so they start from the tip of another branch — producing a **clean, linear history**.

```
Merge:                          Rebase:
A ◀ B ◀ C ◀──── M (main)        A ◀ B ◀ C ◀ D' ◀ E'  (linear!)
       ╲       ╱                       (feature replayed on top of C)
        D ◀ E (feature)
```

```bash
git switch feature
git rebase main          # replay feature's commits on top of main's latest
```

If a conflict appears mid-rebase:
```bash
# fix the conflicted files, then:
git add <files>
git rebase --continue    # proceed to the next commit
git rebase --skip        # skip the current commit
git rebase --abort       # cancel and return to where you started
```

### Rebase vs. Merge — which should I use?

| | **Merge** | **Rebase** |
| --- | --- | --- |
| History | Preserves exactly what happened (with merge commits) | Clean, linear, easy to read |
| Safety on shared branches | ✅ Safe | ⚠️ Only on local/unshared |
| Traceability | Shows true branching | Hides the original branch points |

Many teams **rebase local feature branches** to tidy them, then **merge** into `main` via a Pull Request. Both are valid — it's a team style choice.

---

## Interactive rebase — the cleanup superpower 🧹

`git rebase -i` lets you **edit, reorder, squash, and delete** your recent commits before sharing them. This is how you turn 6 messy "wip", "fix", "oops" commits into 1–2 clean ones.

```bash
git rebase -i HEAD~4     # interactively edit the last 4 commits
```

Git opens an editor listing those commits:
```
pick a1b2c3d Add login form
pick b2c3d4e wip
pick c3d4e5f fix typo
pick d4e5f6a oops forgot file
```

Change the word before each commit to tell Git what to do:

| Command | Does |
| --- | --- |
| `pick` | Keep the commit as-is |
| `reword` | Keep the commit, but edit its **message** |
| `edit` | Pause to amend the commit's **contents** |
| `squash` | Merge into the previous commit, **combining messages** |
| `fixup` | Like squash, but **discard** this commit's message |
| `drop` | **Delete** the commit entirely |
| (reorder lines) | Reorder the commits |

Example — squash the three messy commits into the first:
```
pick   a1b2c3d Add login form
fixup  b2c3d4e wip
fixup  c3d4e5f fix typo
fixup  d4e5f6a oops forgot file
```
Save and close → you now have **one clean commit**: *"Add login form."* ✨

> 💡 The `git commit --fixup <hash>` + `git rebase -i --autosquash` combo automates this: mark fixups as you go, then let Git arrange them.

---

## `git cherry-pick` — grab a specific commit

Copy an individual commit from one branch onto your current branch — useful for hotfixes or pulling one change without merging a whole branch.

```bash
git cherry-pick 9c6c1f4              # apply that commit here
git cherry-pick A^..B                # apply a range of commits
git cherry-pick --no-commit 9c6c1f4  # apply changes but don't commit yet
```

```
main:     A ◀ B ◀ C
                    ╲ cherry-pick X
feature:  … ◀ X ◀ Y      ──▶   main: A ◀ B ◀ C ◀ X'
```

---

## `git revert` vs `reset` vs `rebase` — quick contrast

| Tool | What it does | History |
| --- | --- | --- |
| `revert` | New commit that undoes an old one | Preserved (safe) |
| `reset` | Moves branch pointer back | Rewritten (local) |
| `rebase` | Replays commits onto a new base | Rewritten (local) |

---

## ✅ Key takeaways

- **Golden rule:** never rewrite history others have pulled.
- `git rebase main` gives a **linear** history vs. a merge commit.
- **Interactive rebase** (`-i`) lets you squash/reword/reorder/drop commits — perfect for cleaning a branch before a PR.
- `git cherry-pick` copies a single commit onto your branch.
- Mid-rebase: `--continue`, `--skip`, or `--abort`.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Undoing Changes](07-undoing-changes.md) &nbsp;·&nbsp; Next: [9 · Advanced Git ➡️](09-advanced-git.md)
