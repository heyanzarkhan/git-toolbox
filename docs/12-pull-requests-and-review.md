# 12 · Pull Requests &amp; Review

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: GitHub Essentials](11-github-essentials.md) &nbsp;·&nbsp; Next: [Issues &amp; Collaboration ➡️](13-issues-and-collaboration.md)

---

A **Pull Request (PR)** is a proposal: *"Here are my changes on this branch — please review and merge them into `main`."* PRs are where code review, discussion, and automated checks happen. They're the heart of collaboration on GitHub.

> On GitLab the same thing is called a **Merge Request (MR)** — identical concept.

---

## Opening a Pull Request

```bash
# 1. Branch, commit, and push your work
git switch -c add-search
git commit -am "Add search bar"
git push -u origin add-search
```

Then on GitHub:
- A **"Compare &amp; pull request"** banner appears → click it.
- Set the **base** (where it's merging *into*, e.g. `main`) and **compare** (your branch).
- Write a clear **title** and **description**.
- Click **Create pull request.**

Or do it all from the terminal with the GitHub CLI:
```bash
gh pr create --base main --head add-search --title "Add search bar" --body "Adds a global search component."
gh pr status        # see your PRs
gh pr checkout 42   # check out PR #42 locally to test it
```

---

## Anatomy of a good PR

A reviewable PR is **small, focused, and well-described.**

```markdown
## What &amp; why
Adds a global search bar so users can find products from any page.

## Changes
- New `<SearchBar>` component
- Debounced API calls (300 ms)
- Keyboard shortcut: `/` to focus

## Testing
- [x] Manual: searched on home, product, and cart pages
- [x] Added unit tests for the debounce hook

Closes #128
```

> 🔗 Writing **`Closes #128`** (or `Fixes`, `Resolves`) in the description auto-closes that issue when the PR merges. Magic. ✨

---

## Reviewing code 🔍

Good review is what keeps a codebase healthy. On the **Files changed** tab you can:

- Comment on **specific lines** (hover → click the blue `+`).
- Suggest exact edits with a **suggestion block** — the author can accept it in one click:
  ````markdown
  ```suggestion
  const total = price * quantity;
  ```
  ````
- Submit a review as **Comment**, **Approve** ✅, or **Request changes** 🔁.

**As an author**, respond to comments, push follow-up commits (the PR updates automatically), and **resolve conversations** as you address them.

---

## Draft PRs

Open a **Draft pull request** to share work-in-progress and get early feedback or run CI — it can't be merged until you click **Ready for review.**

```bash
gh pr create --draft
```

---

## Status checks &amp; protection 🛡️

PRs can require **automated checks** to pass before merging — tests, linting, builds via [GitHub Actions](14-github-actions-pages-releases.md). Repos often add **branch protection rules** (Settings → Branches) to `main`:

- ✅ Require a passing CI run
- ✅ Require *N* approving reviews
- ✅ Require branches to be up to date
- 🚫 Block direct pushes to `main`

This guarantees nothing reaches `main` without review + green checks.

---

## Merge strategies

When a PR is approved, you choose **how** it lands:

| Strategy | Result | Best when |
| --- | --- | --- |
| **Create a merge commit** | Keeps every commit + a merge commit | You want full, true history |
| **Squash and merge** | Combines all PR commits into **one** | You want a clean, one-commit-per-feature `main` (very popular) |
| **Rebase and merge** | Replays commits onto `main`, no merge commit | You want linear history without squashing |

```bash
gh pr merge 42 --squash --delete-branch    # squash-merge and tidy up
```

> 💡 **Squash and merge** is the most common choice for teams — it keeps `main`'s history clean and readable, one entry per feature.

---

## ✅ Key takeaways

- A **PR** proposes merging your branch into another, with review + discussion + checks.
- Keep PRs **small and well-described**; use `Closes #123` to auto-close issues.
- Review on the **Files changed** tab: line comments, **suggestions**, Approve / Request changes.
- **Draft PRs** share WIP; **branch protection** enforces reviews &amp; passing CI.
- Pick a merge strategy — **Squash and merge** is the popular default for clean history.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: GitHub Essentials](11-github-essentials.md) &nbsp;·&nbsp; Next: [13 · Issues &amp; Collaboration ➡️](13-issues-and-collaboration.md)
