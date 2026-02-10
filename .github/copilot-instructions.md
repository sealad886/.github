---
# Copilot Instructions Metadata — DO NOT REMOVE
# The coding agent uses this metadata to determine when these instructions need updating.
last_updated_commit: "2d4d40d"
last_updated_date: "2026-02-10"
schema_version: 1
---

# Copilot Coding Agent — Default Instructions

> These instructions are the **default** for all `@sealad886` repositories.
> Individual repos may override them with their own `.github/copilot-instructions.md`.

---

## 0 · Staleness Check — Always Do This First

Before starting any task, check whether these instructions are current:

1. Read the `last_updated_commit` value from the YAML frontmatter above.
2. Run `git log --oneline <last_updated_commit>..HEAD` to list commits since that snapshot.
3. **If there are more than 20 new commits, or the `last_updated_date` is more than 30 days old**, update this file:
   - Perform a fresh analysis of the repository (see §6 below).
   - Rewrite or amend the sections that have changed.
   - Update `last_updated_commit` to the current HEAD SHA and `last_updated_date` to today's date.
   - Commit the updated file as part of your pull request.
4. If the instructions are still current, trust them and proceed without re-exploring unless you find information that is incomplete or incorrect.

---

## 1 · Repository Overview

This is the `sealad886/.github` repository — a special GitHub repo that provides **default community health files** and configurations for every public repository owned by `@sealad886`. Files here are used as fallbacks when a repo does not supply its own version.

| Attribute | Value |
|-----------|-------|
| License | MIT |
| Primary content | Markdown, YAML |
| Build toolchain | None (documentation-only repo) |
| CI workflows | `ci.yml`, `codeql-analysis.yml`, `stale.yml` |

---

## 2 · Build, Test & Lint

This repository has **no application code** — it only contains Markdown docs, YAML configs, and GitHub workflow definitions. There is no build step, test suite, or linter to run locally.

The default CI workflow (`.github/workflows/ci.yml`) is designed for repos that *do* contain code. It conditionally runs only when a `package.json` exists:

- **Lint:** `npm ci && npm run lint --if-present` (Node LTS)
- **Test:** `npm ci && npm test --if-present` (Node 18.x & 20.x matrix)
- **Build:** `npm ci && npm run build --if-present` (Node LTS)

When working on a repo that inherits these workflows, always run `npm ci` before build/lint/test.

For the `.github` repo itself, validation is limited to:
- Ensuring Markdown files are well-formed.
- Ensuring YAML files are valid (workflow syntax, dependabot config).

---

## 3 · Project Layout

```
.github/                          ← GitHub configuration directory
├── FUNDING.yml                   ← Sponsorship links (GitHub Sponsors, Buy Me a Coffee)
├── ISSUE_TEMPLATE/
│   ├── bug_report.md             ← Bug report issue template
│   ├── config.yml                ← Issue template chooser config (blank issues enabled)
│   └── feature_request.md        ← Feature request issue template
├── PULL_REQUEST_TEMPLATE.md      ← Default PR template with checklist
├── copilot-instructions.md       ← THIS FILE — Copilot coding agent instructions
├── dependabot.yml                ← Dependabot config (npm, pip, Docker, GitHub Actions)
└── workflows/
    ├── ci.yml                    ← CI: lint → test → build (conditional on package.json)
    ├── codeql-analysis.yml       ← CodeQL security scanning (weekly + push/PR)
    └── stale.yml                 ← Auto-stale issues/PRs after 60 days, close after 7
CODE_OF_CONDUCT.md                ← Contributor Covenant v2.1
CONTRIBUTING.md                   ← Contribution guidelines (fork → branch → PR flow)
LICENSE                           ← MIT License (Copyright 2025 AC)
README.md                         ← Repo description and contents listing
SECURITY.md                       ← Security policy and vulnerability reporting
```

---

## 4 · Workflows & CI Details

### CI (`.github/workflows/ci.yml`)
- Triggers on push/PR to `main`, `master`, `develop`, and manual dispatch.
- All steps are **conditional** on `hashFiles('**/package.json') != ''` — they are skipped when no `package.json` exists.
- Uses `actions/checkout@v6` and `actions/setup-node@v6`.

### CodeQL (`.github/workflows/codeql-analysis.yml`)
- Runs on push/PR to `main`, `master`, `develop`, weekly on Mondays, and manual dispatch.
- Auto-detects languages; supports JS, Python, Go, Java, Ruby, C++, C#, Swift, Kotlin.
- Uses `github/codeql-action@v4`.

### Stale (`.github/workflows/stale.yml`)
- Runs daily at midnight UTC.
- Issues/PRs are marked stale after **60 days** of inactivity, closed after **7 more days**.
- Exempt labels: `pinned`, `security`, `help-wanted` (issues); `pinned`, `security` (PRs).

### Dependabot (`.github/dependabot.yml`)
- Weekly updates for: npm, pip, Docker, GitHub Actions.
- Reviewer: `sealad886`. Labels: `dependencies`, `automated`.

---

## 5 · Conventions & Preferences

- **Branch naming:** `feature/<name>` for features, `bugfix/<name>` for fixes.
- **Commit messages:** Clear, descriptive, atomic — one logical change per commit.
- **Code style:** Follow the existing style of the project you are contributing to.
- **PR template:** Always fill in the Description, Type of Change, Changes Made, Testing, and Checklist sections.
- **Security issues:** Never report through public issues — use GitHub Security Advisories.
- **Testing:** Add tests for new features; ensure all tests pass before submitting a PR.

---

## 6 · Creating or Updating `copilot-instructions.md` for Any Repository

When you encounter a repository that **does not have** a `.github/copilot-instructions.md`, or when the staleness check (§0) determines the file is out-of-date, follow this procedure to create or refresh it.

### 6.1 — Comprehensive Inventory

Search for and read the following files (when they exist):

1. `README.md`, `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md`, `LICENSE`
2. All files under `.github/` (workflows, templates, configs)
3. All project/build files (`package.json`, `Cargo.toml`, `pyproject.toml`, `Makefile`, `Dockerfile`, etc.)
4. All config/linting files (`.eslintrc*`, `.prettierrc*`, `tsconfig.json`, `.flake8`, `rustfmt.toml`, etc.)
5. Any scripts in `scripts/`, `bin/`, `tools/`, or similar directories
6. Search for `HACK`, `TODO`, `FIXME`, `WORKAROUND` comments to identify known issues

### 6.2 — Validate Build & Test Commands

For each discovered build tool:

1. Run the bootstrap/install command (e.g., `npm ci`, `pip install -e .`, `cargo build`).
2. Run the linter (e.g., `npm run lint`, `flake8`, `cargo clippy`).
3. Run the tests (e.g., `npm test`, `pytest`, `cargo test`).
4. Run the build (e.g., `npm run build`, `cargo build --release`).
5. Note the **exact commands that work**, the **order they must be run in**, any **required environment setup**, and any **errors encountered with workarounds**.
6. Note the approximate time each command takes.
7. Try running commands in different orders and after cleaning (`git clean -fdx`, fresh env) to catch hidden dependencies.

### 6.3 — Write the Instructions

Create `.github/copilot-instructions.md` with the following structure:

```markdown
---
last_updated_commit: "<current HEAD SHA>"
last_updated_date: "<today's date YYYY-MM-DD>"
schema_version: 1
---

# Copilot Coding Agent Instructions

## 0 · Staleness Check — Always Do This First
<Include the staleness check procedure from §0 above>

## 1 · Repository Overview
<Summary of what the repo does, languages, frameworks, runtimes>

## 2 · Build, Test & Lint
<Exact commands in the order they should be run, with versions>

## 3 · Project Layout
<Tree listing of important directories and files, with descriptions>

## 4 · Workflows & CI Details
<Document each GitHub Actions workflow, triggers, and key steps>

## 5 · Conventions & Preferences
<Coding style, branch naming, commit message format, etc.>
```

### 6.4 — Limits & Guidelines

- **Maximum length:** ~2 pages. Be concise but complete.
- **Not task-specific:** Do not include instructions for a particular feature or bug.
- **Trust the instructions:** End the file by telling the agent to trust these instructions and only search the codebase when the instructions are incomplete or found to be incorrect.
- When updating an existing file, you may either do a full rewrite or an incremental update based on `git log --oneline <last_updated_commit>..HEAD`.

---

## 7 · Final Note

**Trust these instructions.** Only perform additional codebase exploration if the information here is incomplete or found to be incorrect during your task. This saves time and reduces unnecessary tool usage.
