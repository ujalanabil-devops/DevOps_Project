# 🚀 Git & GitHub Master Guide

<p align="center">
  <img src="https://img.shields.io/badge/Git-Version%20Control-orange?logo=git" />
  <img src="https://img.shields.io/badge/GitHub-Repository-black?logo=github" />
  <img src="https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-blue" />
</p>

A comprehensive Git & GitHub reference repository containing essential commands, workflows, branching strategies, merge/rebase concepts, and troubleshooting tips.

---

# 📚 Table of Contents

- Repository Setup
- Branch Management
- Commit Workflow
- Merge Workflow
- Pull & Rebase
- Git Reset
- Common Status Messages
- Git Workflow Diagrams
- Best Practices
- Quick Cheat Sheet

---

# 📥 Clone Repository

```bash
git clone <repository-url>
cd <repository-folder>
```

---

# 🌿 Branch Management

## View Branches

```bash
git branch
git branch -r
git branch -a
```

## Create New Branch

```bash
git checkout -b feature-1
```

## Switch Branch

```bash
git checkout main
```

---

# ✍️ Commit Workflow

```bash
git add .
git commit -m "Add new feature"
git push origin feature-1
```

## Add Specific File

```bash
git add filename.txt
```

---

# 🔀 Merge Workflow

```bash
git checkout main
git merge feature-1
git push origin main
```

---

# 📊 Git Workflow Diagram

```text
main
 │
 ├─────●────────●────────●
 │
 └───── feature-1
         │
         ●────●────●
                  │
                  ▼
               merge
```

Development Flow:

```text
Clone Repo
    │
    ▼
Create Branch
    │
    ▼
Make Changes
    │
    ▼
git add
    │
    ▼
git commit
    │
    ▼
git push
    │
    ▼
Merge to Main
```

---

# 🔄 Pull & Rebase

## Standard Pull

```bash
git pull origin main
```

Internally:

```text
git fetch + git merge
```

## Rebase Pull

```bash
git pull --rebase origin main
```

### Rebase Visualization

Before:

```text
A---B---C (origin/main)
     \
      D---E (local)
```

After Rebase:

```text
A---B---C---D'---E'
```

Benefits:

- Cleaner history
- No unnecessary merge commits
- Easier code review

---

# 🔁 Git Reset

Git Reset moves HEAD to a previous commit.

## Soft Reset

```bash
git reset --soft HEAD~1
```

| History | Staging | Files |
|----------|----------|----------|
| ✅ | ✅ | ✅ |

---

## Mixed Reset

```bash
git reset --mixed HEAD~1
```

| History | Staging | Files |
|----------|----------|----------|
| ✅ | ❌ | ✅ |

---

## Hard Reset

```bash
git reset --hard HEAD~1
```

| History | Staging | Files |
|----------|----------|----------|
| ✅ | ❌ | ❌ |

⚠️ Warning: Deletes uncommitted changes permanently.

### Reset Visualization

```text
Commit History

A ← B ← C ← D (HEAD)

git reset --soft HEAD~1

A ← B ← C (HEAD)
```

---

# 🚦 Common Git Status Messages

## Ahead of Remote

```text
Your branch is ahead of 'origin/test' by 2 commits.
```

Solution:

```bash
git push origin test
```

---

## Branches Have Diverged

```text
Your branch and 'origin/test' have diverged.
```

Solution:

```bash
git pull --rebase origin test
git push origin test
```

Visualization:

```text
origin/test

A---B---C

local/test

A---B---D
```

After Rebase:

```text
A---B---C---D
```

---

# 🗑️ Delete Branches

Local:

```bash
git branch -d feature-1
```

Force Delete:

```bash
git branch -D feature-1
```

Remote:

```bash
git push origin --delete feature-1
```

---

# 🏆 Recommended Team Workflow

```text
main
 │
 ├── feature-login
 ├── feature-payment
 ├── feature-profile
 │
 └── Merge → main
```

Commands:

```bash
git pull origin main
git checkout -b feature-name

# development

git add .
git commit -m "Feature completed"
git push -u origin feature-name
```

---

# ⚡ Git Cheat Sheet

```bash
git status
git log --oneline
git branch
git checkout branch-name
git checkout -b new-branch
git add .
git commit -m "message"
git push
git pull
git pull --rebase
git merge branch-name
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

---

# 💡 Best Practices

✅ Commit frequently

✅ Use meaningful commit messages

✅ Pull before starting work

✅ Use feature branches

✅ Review code before merging

✅ Prefer rebase for clean history

❌ Avoid force push unless necessary

❌ Never commit secrets or passwords

---

# 🎯 Learning Outcome

After using this guide, you should be able to:

- Clone repositories
- Create and manage branches
- Commit changes confidently
- Merge and rebase branches
- Resolve divergence issues
- Use reset safely
- Follow a professional Git workflow

---

⭐ If this repository helps you, consider giving it a star.
