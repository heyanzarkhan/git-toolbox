# 5 · Branching &amp; Merging

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Everyday Git](04-everyday-git.md) &nbsp;·&nbsp; Next: [Working with Remotes ➡️](06-working-with-remotes.md)

---

Branching is Git's superpower. It lets you work on a feature, a bugfix, or a wild experiment **in isolation**, without touching the stable version — then merge it back when it's ready. Because a branch is [just a pointer](03-core-concepts.md#head-branches--refs), it's instant and cheap.

---

## Why branch?

```
        feature-login (your experiment)
              │
              ▼
A ◀── B ◀── C ◀── D
        ▲
        │
       main (stays stable &amp; shippable)
```

You build on `feature-login`. If it works, you merge it into `main`. If it doesn't, you delete it — `main` was never affected. 🧪

---

## Creating &amp; switching branches

Modern Git uses `switch` (clearer) and the older `checkout` (still everywhere):

```bash
git branch                      # list local branches (* marks current)
git branch feature-login        # create a branch (but stay where you are)
git switch feature-login        # switch to it

git switch -c feature-login     # create AND switch in one step ✅ (most common)
git checkout -b feature-login   # same thing, older syntax

git switch main                 # go back to main
git switch -                    # switch to the previous branch
```

Rename and delete:
```bash
git branch -m new-name          # rename the current branch
git branch -d feature-login     # delete (safe: refuses if unmerged)
git branch -D feature-login     # force-delete (even if unmerged)
```

---

## Merging

Once your feature is ready, bring it into `main`:

```bash
git switch main                 # 1. go to the branch you want to merge INTO
git merge feature-login         # 2. merge the feature branch into it
```

There are two kinds of merge:

### Fast-forward merge ⏩
If `main` hasn't moved since you branched, Git just slides the `main` pointer forward. No new commit needed.
```
Before:  A ◀ B ◀ C (main) ◀ D ◀ E (feature)
After:   A ◀ B ◀ C ◀ D ◀ E (main, feature)
```

### Three-way merge 🔀
If **both** branches have new commits, Git creates a special **merge commit** with *two* parents, weaving the histories together.
```
A ◀ B ◀ C ◀──── F (main)
          ╲      ╲
           D ◀ E ◀ M (merge commit)
              (feature)
```

Force a merge commit even when a fast-forward is possible (keeps history explicit):
```bash
git merge --no-ff feature-login
```

---

## Merge conflicts (don't panic 😌)

A **conflict** happens when two branches changed the **same lines** of the same file, and Git can't decide which version wins. It pauses and asks you.

You'll see this inside the file:
```diff
<<<<<<< HEAD
const greeting = "Hello";        ← your current branch's version
=======
const greeting = "Hi there";     ← the incoming branch's version
>>>>>>> feature-login
```

### How to resolve a conflict — step by step

1. **See which files conflict:**
   ```bash
   git status        # conflicted files are listed under "Unmerged paths"
   ```
2. **Open each file and edit it** — keep the correct version and **delete the `<<<<<<<`, `=======`, `>>>>>>>` markers** entirely.
   ```js
   const greeting = "Hello there";   // your reconciled result
   ```
3. **Stage the resolved files:**
   ```bash
   git add greeting.js
   ```
4. **Complete the merge:**
   ```bash
   git commit        # finishes the merge (message is pre-filled)
   ```

### Escape hatches
```bash
git merge --abort     # cancel the merge, return to the pre-merge state
```

> 🛠️ A visual merge tool can make conflicts much easier: `git mergetool`. Editors like VS Code also show conflicts with handy "Accept Current / Incoming / Both" buttons.

---

## A complete branch → merge example

```bash
git switch -c add-footer        # create & switch
# ...edit files...
git add .
git commit -m "Add site footer"

git switch main                 # back to main
git merge add-footer            # merge it in
git branch -d add-footer        # clean up the merged branch
```

---

## ✅ Key takeaways

- A branch is a cheap, movable pointer — branch **freely**.
- `git switch -c name` creates and switches in one go.
- Merge **into** the target: `switch main`, then `merge feature`.
- **Fast-forward** = pointer slides forward; **three-way** = a merge commit with two parents.
- A **conflict** just means "you decide" — edit the file, remove the markers, `add`, then `commit`. `git merge --abort` bails out.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Everyday Git](04-everyday-git.md) &nbsp;·&nbsp; Next: [6 · Working with Remotes ➡️](06-working-with-remotes.md)
