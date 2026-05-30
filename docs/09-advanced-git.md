# 9 · Advanced Git

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Rewriting History](08-rewriting-history.md) &nbsp;·&nbsp; Next: [Command Reference ➡️](10-command-reference.md)

---

A tour of Git's power tools — the commands that make you look like a wizard 🧙 to your teammates.

---

## `git stash` — shelve work temporarily

You're mid-feature and need to switch branches *right now* for an urgent fix — but you're not ready to commit. **Stash** it:

```bash
git stash                          # shelve all tracked changes, clean the working dir
git stash push -m "half-done nav"  # stash with a label
git stash -u                       # include untracked files too

git stash list                     # see all stashes
# stash@{0}: On feature: half-done nav

git stash apply                    # re-apply the latest stash (keeps it in the list)
git stash pop                      # re-apply AND remove it from the list
git stash apply stash@{2}          # apply a specific stash
git stash drop stash@{0}           # delete one stash
git stash clear                    # delete all stashes
```

> 💡 Stash is for **short-term** context switches, not long-term storage. For anything you want to keep, make a commit on a branch instead.

---

## `git tag` — mark releases 🏷️

Tags name a specific commit — almost always used to mark **release versions** (`v1.0.0`).

```bash
git tag                            # list tags
git tag v1.0.0                     # lightweight tag (just a name)
git tag -a v1.0.0 -m "First release"   # annotated tag (recommended: has author/date/message)
git tag -a v1.0.0 9c6c1f4          # tag a specific past commit
git show v1.0.0                    # see what a tag points to

git push origin v1.0.0             # push one tag (tags are NOT pushed by default!)
git push --tags                    # push all tags
git tag -d v1.0.0                  # delete a local tag
git push origin --delete v1.0.0    # delete a remote tag
```

> 📦 **Annotated tags** (`-a`) store who/when/why and are what GitHub turns into **Releases**. Prefer them for anything public.

---

## `git bisect` — binary-search for a bug 🔍

A bug appeared *somewhere* in the last 200 commits. Instead of checking each one, `bisect` does a binary search — ~8 checks instead of 200.

```bash
git bisect start
git bisect bad                 # the current commit is broken
git bisect good v1.0.0         # this old version worked
# Git checks out a commit halfway between. Test it, then tell Git:
git bisect good                # ...if this one works
git bisect bad                 # ...if it's broken
# Repeat until Git pinpoints the exact commit that introduced the bug:
# → "abc123 is the first bad commit"
git bisect reset               # return to where you started
```

You can even automate it: `git bisect run ./test.sh`. 🤖

---

## `git worktree` — multiple branches checked out at once

Normally a repo has one working directory. **Worktrees** let you check out several branches into separate folders simultaneously — no stashing, no re-cloning.

```bash
git worktree add ../project-hotfix hotfix   # check out 'hotfix' in a sibling folder
git worktree list                           # show all worktrees
git worktree remove ../project-hotfix       # clean up when done
```

Great for reviewing a PR while keeping your feature work untouched.

---

## Submodules — a repo inside a repo

A **submodule** embeds another Git repository inside yours at a pinned commit (e.g. a shared library).

```bash
git submodule add https://github.com/user/lib.git libs/lib   # add one
git clone --recurse-submodules <url>          # clone a repo + its submodules
git submodule update --init --recursive       # fetch submodules after a normal clone
git submodule update --remote                 # update submodules to their latest
```

> ⚠️ Submodules are powerful but add complexity — every clone must remember to init them. Use deliberately.

---

## Git hooks — automate on events 🪝

Hooks are scripts Git runs automatically at certain points (before a commit, before a push, etc.). They live in `.git/hooks/`.

```bash
# .git/hooks/pre-commit  (make it executable: chmod +x)
#!/bin/sh
npm run lint || exit 1     # block the commit if linting fails
```

Common hooks: `pre-commit` (lint/format/test before committing), `commit-msg` (enforce message format), `pre-push` (run tests before pushing). Tools like **Husky** manage hooks in a shareable, versioned way.

---

## Maintenance &amp; housekeeping 🧰

```bash
git gc                       # garbage-collect & compress the repo
git fsck                     # check repository integrity
git count-objects -vH        # see how much space the repo uses
git remote prune origin      # drop stale remote-tracking branches
git log --all --oneline --graph   # visualize the entire history
```

---

## ✅ Key takeaways

- `git stash` shelves changes for quick context switches; `pop` re-applies and removes.
- `git tag -a` makes annotated tags for releases — and remember to `push --tags`.
- `git bisect` binary-searches your history to find the commit that broke something.
- `git worktree` checks out multiple branches into separate folders at once.
- **Submodules** nest repos; **hooks** automate actions on Git events.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Rewriting History](08-rewriting-history.md) &nbsp;·&nbsp; Next: [10 · Command Reference ➡️](10-command-reference.md)
