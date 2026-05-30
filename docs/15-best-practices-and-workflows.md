# 15 · Best Practices &amp; Workflows

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Actions, Pages &amp; Releases](14-github-actions-pages-releases.md) &nbsp;·&nbsp; Next: [Troubleshooting ➡️](16-troubleshooting.md)

---

Knowing the commands is one thing; using them like a pro is another. This chapter is the "good habits" guide that separates tidy, collaborative repos from chaotic ones.

---

## Writing great commit messages ✍️

A commit message explains **why** a change happened — your future teammates (and future you) will thank you.

**The 7 rules of a great commit message:**
1. Separate **subject** from **body** with a blank line.
2. Limit the subject to **~50 characters**.
3. Use the **imperative mood**: *"Add login"*, not *"Added login"* or *"Adds login"*.
4. **Capitalize** the subject; **no period** at the end.
5. Use the **body** to explain *what* and *why* (not *how*).
6. **Wrap** the body at ~72 characters.
7. **Reference issues**: `Closes #128`.

```
Add rate limiting to the login endpoint

Brute-force attempts were possible because there was no throttle.
Limit to 5 attempts per IP per minute, returning HTTP 429 after that.

Closes #142
```

### Conventional Commits 📐
A popular, machine-readable convention — great because it can **auto-generate changelogs** and version bumps:

```
<type>(optional scope): <description>

feat:     a new feature              fix:      a bug fix
docs:     documentation only         refactor: code change, no behavior change
test:     adding/fixing tests        chore:    tooling, deps, config
perf:     a performance improvement  style:    formatting only
```
Examples: `feat(auth): add password reset`, `fix: handle empty cart`, `docs: clarify install steps`.

---

## Atomic commits ⚛️

**One logical change per commit.** Don't mix a bug fix, a refactor, and a typo correction into one commit. Atomic commits are easier to review, revert, and `cherry-pick`. Use `git add -p` to split work into clean pieces.

---

## Branch naming conventions 🌿

Consistent names keep a busy repo readable:

```
feature/search-bar       feat/  → new work
fix/login-crash          bug/   → bug fixes
hotfix/payment-timeout   hotfix/→ urgent production fixes
chore/upgrade-deps       chore/ → maintenance
docs/api-guide           docs/  → documentation
```
Some teams add issue numbers: `feature/142-search-bar`.

---

## The three big branching models

How a team organizes branches. Pick one and be consistent.

### 1. GitHub Flow — simple &amp; continuous ⭐
```
main ─●─────●─────●─────●──   (always deployable)
       ╲   ╱ ╲   ╱
        ●─●   ●─●            (short-lived feature branches → PR → merge)
```
- One long-lived branch: **`main`** (always shippable).
- Every change is a **short-lived branch → PR → review → merge → deploy**.
- ✅ Best for web apps &amp; continuous deployment. **Recommended default for most teams.**

### 2. Git Flow — structured releases
```
main      ──●──────────────●────  (production; tagged releases)
release   ────●────●────────
develop   ─●───●────●────●────●──  (integration branch)
feature   ──●─●──────●─●─────────  (off develop)
```
- Multiple long-lived branches: `main`, `develop`, plus `feature/*`, `release/*`, `hotfix/*`.
- ✅ Good for **versioned software with scheduled releases**; ⚠️ heavier, often overkill for web apps.

### 3. Trunk-Based Development — fast &amp; lean
```
main ─●─●─●─●─●─●─●──   everyone commits to main (behind feature flags)
```
- Everyone integrates into **`main`** many times a day; very short branches.
- ✅ Enables true continuous delivery at scale; relies heavily on automated tests &amp; **feature flags**.

| Model | Long-lived branches | Best for |
| --- | --- | --- |
| **GitHub Flow** | `main` only | Most teams, web apps, CD |
| **Git Flow** | `main` + `develop` | Scheduled, versioned releases |
| **Trunk-Based** | `main` only | High-velocity teams with strong CI |

---

## `.gitignore` discipline 🙈

- Ignore **dependencies** (`node_modules/`), **build output** (`dist/`), **secrets** (`.env`), and **OS/editor junk** (`.DS_Store`, `.idea/`).
- Start from a template: **[github.com/github/gitignore](https://github.com/github/gitignore)** has one for every language.
- Already committed something you shouldn't have? `git rm --cached <file>`, then ignore it.

---

## 🔐 Never commit secrets

API keys, passwords, and tokens **do not belong in Git** — once pushed, assume they're compromised forever (history is public/clonable).

- Keep secrets in **`.env`** files (git-ignored) or a secrets manager.
- Use **GitHub Secrets** for CI ([Chapter 14](14-github-actions-pages-releases.md)).
- Enable **Secret Scanning** &amp; **push protection** (Settings → Security).
- Leaked one? **Rotate the key immediately**, then scrub history with `git filter-repo` or the [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/). (See [Troubleshooting](16-troubleshooting.md).)

---

## Pull request etiquette 🤝

- **Small PRs** get reviewed faster and better than giant ones.
- Write a clear description; link the issue (`Closes #X`).
- Respond to every review comment; resolve threads as you go.
- As a reviewer: be **kind, specific, and timely**; use `suggestion` blocks; approve when it's good enough, not perfect.

---

## ✅ Key takeaways

- Write **imperative, focused** commit messages; consider **Conventional Commits**.
- Keep commits **atomic** — one logical change each.
- Use **consistent branch names** and a clear **branching model** (GitHub Flow suits most teams).
- Be disciplined with **`.gitignore`** and **never commit secrets**.
- Keep PRs small and reviews kind.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Actions, Pages &amp; Releases](14-github-actions-pages-releases.md) &nbsp;·&nbsp; Next: [16 · Troubleshooting ➡️](16-troubleshooting.md)
