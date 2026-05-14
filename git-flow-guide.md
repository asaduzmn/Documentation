# Git Flow — Personal Reference Guide

## Overview

Git Flow is a branching model that defines a strict branching structure for managing releases, features, hotfixes, and support branches. It sits on top of Git and uses `git flow` CLI commands as shortcuts.

---

## Installation

```bash
sudo apt install git-flow
```

---

## Initialization

Run once per repo to configure branch naming conventions:

```bash
git flow init
```

### Configuration used in `sms-gateway-admin`

| Prompt | Value |
|---|---|
| Production releases branch | `master` |
| Next release (integration) branch | `main` |
| Feature branch prefix | `feat/` |
| Bugfix branch prefix | `bugfix/` |
| Release branch prefix | `release/` |
| Hotfix branch prefix | `hotfix/` |
| Support branch prefix | `support/` |
| Version tag prefix | *(empty)* |
| Hooks directory | `.git/hooks` |

---

## Branch Structure

```
master       ← production-ready code (stable)
main         ← integration branch (next release)
feat/*       ← feature development
bugfix/*     ← bug fixes on development branch
release/*    ← release preparation
hotfix/*     ← urgent fixes directly on master
support/*    ← long-term support branches
```

---

## Feature Branches

Used for all new features and non-urgent changes.

### Start a feature

```bash
git flow feature start <branch-name>
# Creates: feat/<branch-name> based off main
```

**Example:**
```bash
git flow feature start cn_86evgrnhk_update_migration_files
# → Switched to a new branch 'feat/cn_86evgrnhk_update_migration_files'
```

### Finish a feature

```bash
git flow feature finish <branch-name>
# Merges feat/<branch-name> → main, deletes the feature branch
```

### Publish a feature (push to remote)

```bash
git flow feature publish <branch-name>
```

### Pull a remote feature

```bash
git flow feature pull origin <branch-name>
```

---

## Bugfix Branches

Used for bug fixes on the development/integration branch (`main`).

```bash
# Start
git flow bugfix start <branch-name>

# Finish
git flow bugfix finish <branch-name>
```

---

## Release Branches

Used to prepare a new production release (version bumps, changelog, etc.).

```bash
# Start
git flow release start <version>
# Example:
git flow release start 1.2.0

# Finish (merges into master AND main, creates a tag)
git flow release finish 1.2.0
```

---

## Hotfix Branches

Used for critical production fixes directly off `master`.

```bash
# Start (branches off master)
git flow hotfix start <version>
# Example:
git flow hotfix start 1.2.1

# Finish (merges into master AND main, creates a tag)
git flow hotfix finish 1.2.1
```

---

## Quick Command Reference

| Action | Command |
|---|---|
| Init git flow | `git flow init` |
| Start feature | `git flow feature start <name>` |
| Finish feature | `git flow feature finish <name>` |
| Publish feature | `git flow feature publish <name>` |
| Start bugfix | `git flow bugfix start <name>` |
| Finish bugfix | `git flow bugfix finish <name>` |
| Start release | `git flow release start <version>` |
| Finish release | `git flow release finish <version>` |
| Start hotfix | `git flow hotfix start <version>` |
| Finish hotfix | `git flow hotfix finish <version>` |
| List features | `git flow feature list` |
| List releases | `git flow release list` |

---

## Naming Convention

Branch names in this project follow the pattern:

```
feat/<ticket-id>_<short-description>
```

**Example:**
```
feat/cn_86evgrnhk_update_migration_files
```

---

## Notes

- Always branch off `main` for new features — never off `master` directly.
- `git flow feature finish` deletes the local feature branch automatically.
- For remote collaboration, always `publish` the feature before finishing it.
- Hotfixes are the only branches that can branch off `master`.
