# 13 · Issues &amp; Collaboration

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Pull Requests &amp; Review](12-pull-requests-and-review.md) &nbsp;·&nbsp; Next: [Actions, Pages &amp; Releases ➡️](14-github-actions-pages-releases.md)

---

Code is only half of GitHub — the other half is **coordinating people**: tracking work, planning, discussing, and managing who can do what. This chapter covers the collaboration toolkit.

---

## Issues 🐛

An **issue** is a tracked unit of work — a bug, a feature request, a question, or a task. Issues are the to-do list of your project.

**A good issue:**
```markdown
**Title:** Search returns no results for accented characters

**Describe the bug**
Searching "café" returns nothing, but "cafe" works.

**Steps to reproduce**
1. Go to /search
2. Type "café"
3. See "No results"

**Expected:** accent-insensitive matching.
**Environment:** Chrome 124, app v2.3.1
```

Issues support **Markdown**, `@mentions`, task lists (`- [ ]`), and references to other issues/PRs by `#number`.

```bash
gh issue create --title "Fix accent search" --body "..."
gh issue list --label bug
gh issue close 128
```

---

## Labels, milestones &amp; assignees 🏷️

Organize issues and PRs with:

| Tool | Purpose |
| --- | --- |
| **Labels** | Categorize: `bug`, `enhancement`, `good first issue`, `priority: high` |
| **Assignees** | Who's responsible |
| **Milestones** | Group issues toward a goal/release (e.g. *v2.0*), with a due date &amp; progress bar |
| **Projects** | Visual planning across many issues (below) |

> 🌱 The **`good first issue`** label is a convention that helps newcomers find approachable tasks — great for welcoming open-source contributors.

---

## Projects (planning boards) 📋

**GitHub Projects** are flexible boards (Kanban, table, or roadmap views) that pull in issues and PRs so you can plan and track status:

```
┌─ To do ──┐  ┌─ In progress ┐  ┌─ Done ────┐
│ #128 bug │  │ #131 search  │  │ #120 login│
│ #129 docs│  │              │  │ #122 nav  │
└──────────┘  └──────────────┘  └───────────┘
```

Cards move across columns as work progresses, and custom fields (priority, size, sprint) let you slice the data however you like.

---

## Discussions 💬

**Discussions** are for conversation that isn't a task: Q&amp;A, ideas, announcements, show-and-tell. Unlike issues, they're threaded and can have **accepted answers** (the **Q&amp;A** category).

| Use an **Issue** when… | Use a **Discussion** when… |
| --- | --- |
| There's actionable work to track | You want open-ended conversation |
| It can be "closed" when done | It's a question, idea, or announcement |
| It belongs on a board | It's community Q&amp;A |

> 💡 In a **Q&amp;A** discussion, the asker (or a maintainer) can mark a reply as the **accepted answer** — and the answer's author earns the *Galaxy Brain* achievement.

---

## Mentions, references &amp; cross-linking 🔗

GitHub auto-links these everywhere (issues, PRs, comments, commit messages):

| You type | GitHub does |
| --- | --- |
| `@username` | Notifies and links that person |
| `@org/team` | Notifies a whole team |
| `#128` | Links to issue/PR #128 |
| `Closes #128` in a PR | Auto-closes #128 when merged |
| `user/repo#42` | Links a PR/issue in another repo |
| a commit SHA | Links to that commit |

---

## Managing access &amp; teams 👥

| Scope | How access works |
| --- | --- |
| **Personal repo** | Add individual **collaborators** (Settings → Collaborators) |
| **Organization** | Group people into **teams**; grant teams repo permissions |

**Permission levels:** **Read** (view/clone) · **Triage** (manage issues/PRs) · **Write** (push) · **Maintain** (manage settings) · **Admin** (full control).

> 🔐 Use **CODEOWNERS** (a file at `.github/CODEOWNERS`) to auto-request reviews from the right people when matching files change.

---

## Templates 📝

Standardize contributions with files in `.github/`:

- `.github/ISSUE_TEMPLATE/` — prefilled forms for bug reports / feature requests
- `.github/PULL_REQUEST_TEMPLATE.md` — a checklist every PR starts with
- `CONTRIBUTING.md` — how to contribute
- `CODE_OF_CONDUCT.md` — community standards

---

## ✅ Key takeaways

- **Issues** track actionable work; organize them with **labels**, **milestones**, and **assignees**.
- **Projects** are boards (Kanban/table/roadmap) for planning across issues &amp; PRs.
- **Discussions** are for Q&amp;A and open conversation; Q&amp;A answers can be **accepted**.
- `@mentions`, `#123`, and `Closes #123` cross-link and automate everywhere.
- Manage access via **collaborators**, **teams**, permission levels, and **CODEOWNERS**.

---

> 🏠 [Handbook Home](../README.md) &nbsp;·&nbsp; ⬅️ [Prev: Pull Requests &amp; Review](12-pull-requests-and-review.md) &nbsp;·&nbsp; Next: [14 · Actions, Pages &amp; Releases ➡️](14-github-actions-pages-releases.md)
