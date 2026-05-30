# 11 · GitHub Essentials

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Command Reference](10-command-reference.md) &nbsp;·&nbsp; Next: [Pull Requests &amp; Review ➡️](12-pull-requests-and-review.md)

---

You now know **Git** (the tool). **GitHub** is the most popular place to *host* Git repositories and collaborate around them. This part of the handbook covers the GitHub-specific layer that sits on top of Git.

> Remember the distinction from [Chapter 1](01-what-is-git.md#git--github-): Git runs on your machine; GitHub lives in the cloud. Everything here also has close equivalents on **GitLab** and **Bitbucket**.

---

## Anatomy of a GitHub repository

When you open a repo on GitHub, you'll see these tabs:

| Tab | What it's for |
| --- | --- |
| **Code** | The files, README, branches, and releases |
| **Issues** | Bug reports, feature requests, to-dos |
| **Pull requests** | Proposed changes under review ([Chapter 12](12-pull-requests-and-review.md)) |
| **Actions** | Automated workflows / CI-CD ([Chapter 14](14-github-actions-pages-releases.md)) |
| **Projects** | Kanban boards &amp; planning ([Chapter 13](13-issues-and-collaboration.md)) |
| **Wiki** | Long-form documentation |
| **Security** | Vulnerability alerts, policies |
| **Insights** | Contributor stats &amp; graphs |
| **Settings** | Configuration (admins only) |

The **README.md** is the front page — it renders automatically. A great README is the difference between a repo people star and one they scroll past. (You're reading a pretty good one right now. 😉)

---

## Creating &amp; connecting a repo

**On GitHub:** click **+ → New repository**, give it a name, and create it.

**Connect a local project to it:**
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:you/repo.git
git push -u origin main
```

**Or start from GitHub** by cloning the empty repo and working inside it.

> ⚡ The **GitHub CLI** (`gh`) does this in one step: `gh repo create my-project --public --source=. --push`.

---

## Public vs. Private

| | **Public** | **Private** |
| --- | --- | --- |
| Who can see it | Anyone | Only you + invited collaborators |
| Good for | Open source, portfolios | Client work, secrets, WIP |
| Free? | Yes | Yes (with generous limits) |

You can flip between them anytime in **Settings → General → Danger Zone**.

---

## Forking 🍴

A **fork** is *your own copy* of someone else's repository, under your account. It's the foundation of open-source contribution: you can't push to a stranger's repo, but you *can* fork it, change your fork, and propose your changes back via a Pull Request.

**The fork-and-PR flow:**
```bash
# 1. Click "Fork" on GitHub → you now have github.com/you/their-repo
# 2. Clone YOUR fork
git clone git@github.com:you/their-repo.git
cd their-repo
# 3. Add the ORIGINAL as 'upstream' so you can stay in sync
git remote add upstream git@github.com:original/their-repo.git
# 4. Create a branch, make changes, push to YOUR fork
git switch -c fix-typo
git commit -am "Fix typo in docs"
git push -u origin fix-typo
# 5. Open a Pull Request from your fork → the original repo
```

**Keep your fork up to date:**
```bash
git fetch upstream
git switch main
git merge upstream/main      # or: git rebase upstream/main
git push                     # update your fork
```

---

## The GitHub Flow 🔄

The simple, popular branching workflow GitHub itself recommends:

```
1. Branch     → create a branch off main for your work
2. Commit     → make changes in small commits
3. Push       → publish your branch to GitHub
4. Pull Request → open a PR to propose merging into main
5. Review     → teammates review &amp; discuss
6. Merge      → merge into main (main is always deployable)
7. Delete     → delete the branch
```

`main` is **always kept in a working, shippable state.** All work happens on short-lived branches that get reviewed before merging. More workflows in [Chapter 15](15-best-practices-and-workflows.md).

---

## Your GitHub profile ⭐

A few touches that make your profile shine:

- **Profile README** — create a repo named exactly your username (e.g. `heyanzarkhan/heyanzarkhan`) with a `README.md`; it shows on your profile page.
- **Pin** your best repositories.
- **Achievements** — badges like *Pull Shark*, *Galaxy Brain*, *Starstruck*, earned through activity.
- **Stars** — bookmark repos you love; a repo's star count is its popularity signal.

---

## ✅ Key takeaways

- GitHub *hosts* Git repos and adds Issues, Pull Requests, Actions, and more.
- Connect a local repo with `git remote add origin … && git push -u origin main`.
- **Fork** to copy someone's repo to your account; sync with an `upstream` remote.
- The **GitHub Flow** = branch → commit → push → PR → review → merge → delete.
- A strong **README** and **profile** make your work discoverable.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Command Reference](10-command-reference.md) &nbsp;·&nbsp; Next: [12 · Pull Requests &amp; Review ➡️](12-pull-requests-and-review.md)
