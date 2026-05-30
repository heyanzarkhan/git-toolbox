# 16 · Troubleshooting

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Best Practices &amp; Workflows](15-best-practices-and-workflows.md) &nbsp;·&nbsp; Next: [Glossary ➡️](17-glossary.md)

---

Real error messages and how to fix them. `Ctrl/Cmd + F` for the text you're seeing. 🔧

---

## "fatal: not a git repository"
You're not inside a Git repo. Either `cd` into one, or initialize:
```bash
git init
```

---

## "Updates were rejected because the remote contains work that you do not have"
Someone pushed before you. **Pull first**, then push:
```bash
git pull --rebase     # bring in their changes, replay yours on top
git push
```

---

## "Your branch and 'origin/main' have diverged"
Both sides have new commits. Reconcile:
```bash
git pull --rebase     # linear: replay your commits on top of theirs
# or
git pull --no-rebase  # creates a merge commit
```

---

## I'm in 'detached HEAD' state 😱
You checked out a commit/tag directly, so `HEAD` points at a commit instead of a branch. Nothing's broken — just make a branch if you want to keep work here:
```bash
git switch -c my-new-branch   # keep your position on a real branch
git switch main               # ...or just go back, abandoning detached work
```

---

## I committed to `main` but meant to use a branch
Move the commit(s) to a new branch and reset `main`:
```bash
git branch feature-x          # bookmark the current commit on a new branch
git reset --hard origin/main  # rewind main to the remote (⚠️ discards local main changes)
git switch feature-x          # your work is safe here
```

---

## I committed a secret (password/API key) 🔑
1. **Rotate/revoke the secret immediately** — assume it's compromised.
2. Remove it from **all of history** (not just the latest commit):
   ```bash
   # Recommended: git-filter-repo (install separately)
   git filter-repo --path .env --invert-paths
   # Or the BFG Repo-Cleaner:
   bfg --delete-files .env
   ```
3. Force-push the cleaned history and tell collaborators to re-clone.

---

## "Permission denied (publickey)"
Your SSH key isn't set up or recognized. Test and fix:
```bash
ssh -T git@github.com         # diagnose
ssh-add ~/.ssh/id_ed25519     # ensure the key is loaded
# then confirm the public key is added in GitHub → Settings → SSH keys
```
See [Chapter 2](02-installation-and-setup.md#connecting-to-github-securely-ssh).

---

## Wrong author name/email on a commit
Fix the most recent commit:
```bash
git commit --amend --author="Anzar Khan <you@example.com>" --no-edit
```
Fix it everywhere going forward by [setting your config](02-installation-and-setup.md#first-time-configuration).

---

## "refusing to merge unrelated histories"
Two repos with no common history (common when adding a remote to an existing local repo):
```bash
git pull origin main --allow-unrelated-histories
```

---

## I need to undo a commit I already pushed
Don't `reset` shared history — **revert** it:
```bash
git revert <hash>     # safe: creates a new commit that undoes it
git push
```

---

## A huge file is rejected ("file is X MB; this exceeds GitHub's limit")
GitHub blocks files over 100 MB. Remove it from the commit, and use **Git LFS** for large assets:
```bash
git rm --cached big-video.mp4
echo "big-video.mp4" >> .gitignore
# For files you DO need versioned:
git lfs install
git lfs track "*.psd"
```

---

## Line-ending warnings (CRLF/LF)
Windows vs. Unix line endings. Normalize with a `.gitattributes` file:
```gitattributes
* text=auto
```
And configure:
```bash
git config --global core.autocrlf true    # Windows
git config --global core.autocrlf input   # macOS/Linux
```

---

## I accidentally `git add`ed everything
```bash
git restore --staged .        # unstage all (keeps your edits)
```

---

## I deleted a branch / lost commits — can I get them back?
Almost always **yes** — the [reflog](07-undoing-changes.md#git-reflog--your-time-machine-) remembers:
```bash
git reflog                    # find the lost commit's hash
git switch -c recovered <hash>
```

---

## "fatal: remote origin already exists"
```bash
git remote set-url origin <new-url>   # update it
# or
git remote remove origin && git remote add origin <url>
```

---

## ✅ Key takeaways

- Most "rejected push" errors mean **pull first** (`git pull --rebase`).
- **Detached HEAD** is harmless — `git switch -c` to keep work.
- Undo **pushed** commits with `revert`, never `reset`.
- Leaked a secret? **Rotate it**, then scrub history with `git filter-repo`/BFG.
- Lost something? **`git reflog`** is your safety net.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Best Practices &amp; Workflows](15-best-practices-and-workflows.md) &nbsp;·&nbsp; Next: [17 · Glossary ➡️](17-glossary.md)
