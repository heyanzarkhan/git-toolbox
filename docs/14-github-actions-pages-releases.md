# 14 · Actions, Pages &amp; Releases

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Issues &amp; Collaboration](13-issues-and-collaboration.md) &nbsp;·&nbsp; Next: [Best Practices &amp; Workflows ➡️](15-best-practices-and-workflows.md)

---

This chapter covers the "automate &amp; ship" side of GitHub: running tests automatically (**Actions**), hosting websites for free (**Pages**), and publishing versions (**Releases**).

---

## GitHub Actions — automation &amp; CI/CD ⚙️

**Actions** run automated **workflows** when something happens in your repo — a push, a PR, a schedule. This is how you do **CI/CD**:

- **CI (Continuous Integration):** automatically build &amp; test every change.
- **CD (Continuous Deployment):** automatically deploy when tests pass.

Workflows are YAML files in **`.github/workflows/`**. Here's a complete CI example that runs tests on every push and PR:

```yaml
# .github/workflows/ci.yml
name: CI

on:                       # WHEN to run
  push:
    branches: [main]
  pull_request:

jobs:                     # WHAT to run
  test:
    runs-on: ubuntu-latest        # the machine
    steps:
      - uses: actions/checkout@v4         # 1. get the code
      - uses: actions/setup-node@v4       # 2. set up Node
        with:
          node-version: 20
      - run: npm ci                       # 3. install deps
      - run: npm test                     # 4. run tests
```

### Key concepts

| Term | Meaning |
| --- | --- |
| **Workflow** | An automated process (one YAML file) |
| **Event** (`on:`) | What triggers it (`push`, `pull_request`, `schedule`, `workflow_dispatch`) |
| **Job** | A set of steps that run on one machine |
| **Step** | A single task — a shell command (`run:`) or an action (`uses:`) |
| **Action** | A reusable unit, e.g. `actions/checkout@v4` |
| **Runner** | The machine the job runs on (`ubuntu-latest`, `windows-latest`, `macos-latest`) |
| **Secret** | Encrypted value (API keys) in Settings → Secrets, used as `${{ secrets.NAME }}` |

The green ✅ / red ❌ check you see on commits and PRs comes from these workflows — and can be **required** before merging (see [branch protection](12-pull-requests-and-review.md#status-checks--protection-)).

> 🔎 Browse ready-made actions at the **[GitHub Marketplace](https://github.com/marketplace)** — there's one for almost everything (deploy, lint, release, notify).

---

## GitHub Pages — free static hosting 🌐

**Pages** hosts a website *straight from your repo* — free. Perfect for docs, portfolios, project sites, and landing pages.

**Enable it:** Settings → **Pages** → pick a branch (e.g. `main` / `/docs` folder) → Save. Your site goes live at:
```
https://<username>.github.io/<repo>/
```

- Plain HTML/CSS/JS works instantly.
- Static-site generators like **Jekyll** (built-in), **Hugo**, **Astro**, or **Next.js** export are common.
- Add a `CNAME` file (or configure DNS) for a **custom domain**.
- Deploy via an Action for full control (the `actions/deploy-pages` flow).

---

## Releases &amp; tags 🚀

A **Release** packages a specific version of your project for users to download — built on top of a Git **[tag](09-advanced-git.md#git-tag--mark-releases-)**.

**Create one:**
```bash
git tag -a v1.2.0 -m "Add search + dark mode"
git push origin v1.2.0
# then on GitHub: Releases → Draft a new release → pick the tag
# or with the CLI:
gh release create v1.2.0 --title "v1.2.0" --notes "Adds search and dark mode."
gh release create v1.2.0 ./build/app.zip   # attach downloadable binaries
```

- Follow **[Semantic Versioning](https://semver.org)**: `MAJOR.MINOR.PATCH` (e.g. `2.1.4`) — breaking / feature / fix.
- GitHub can **auto-generate release notes** from merged PRs.
- Attach **assets** (zips, installers) for users to download.

---

## Packages &amp; Codespaces (bonus) 📦

| Feature | What it does |
| --- | --- |
| **GitHub Packages** | Host packages (npm, Docker, Maven…) alongside your code |
| **Codespaces** | A full VS Code dev environment in the browser — code without local setup |
| **Dependabot** | Auto-opens PRs to update vulnerable/outdated dependencies |

---

## ✅ Key takeaways

- **Actions** run YAML **workflows** in `.github/workflows/` on events like `push`/`pull_request` — your CI/CD.
- A workflow has **jobs** → **steps**, running on **runners**; secrets stay encrypted.
- **Pages** hosts a static site free at `username.github.io/repo`.
- **Releases** wrap a Git **tag** into a downloadable version — use **SemVer**.
- Bonus: **Packages**, **Codespaces**, and **Dependabot** round out the platform.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Issues &amp; Collaboration](13-issues-and-collaboration.md) &nbsp;·&nbsp; Next: [15 · Best Practices &amp; Workflows ➡️](15-best-practices-and-workflows.md)
